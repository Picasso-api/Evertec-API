# Enviar un token de autenticación

Ahora que tiene un token de autenticación debe enviarlo al invocar cualquier operación en la **API**. Lo único que debe hacer es agregarlo al Payload de la solicitud. Así de simple.

Veamos un ejemplo:

Creemos una operación para consultar los tipos de identificación registrados en la **API**

Primero, definamos una clase que represente la información de un Tipo de identificación en el sistema:

```csharp
public class DocType
{
    public string ShortName { get; set; }
    public string Name { get; set; }
    public int Id { get; set; }
    public int Order { get; set; }
}
```

Ahora, agreguemos una operación a la definición del servicio que represente la operación  para obtener la lista de tipos de documento del sistema `GetDocTypes`.

```csharp
public interface IEvertecAPIService
{
    AuthContext AuthContext {get;}
    void Signin();
    IList<DocType> GetDocTypes();
}
```

Y, finalmente agreguemos la operación en la clase `EvertecAPIService`.

<div class="admonition warning">
   <p class="first admonition-title">Payload/Token</p>
   <p class="last">Observe que estamos enviando en el Payload el valor del Token.</p>
</div>

```csharp
public IList<DocType> GetDocTypes()
{
    var payload = new Dictionary<string, object>
    {
        { "Nonce", this.nonceProvider.GetNonce() },
        { "Epoch", this.epochProvider.GetSeconds() },
        { "Token", this.AuthContext.Token }
    };

    IRestRequest request = new RestRequest("/app/resx/document-types", Method.GET);
    request.AddHeader("X-PRO-Auth-App", this.appKey);
    request.AddHeader("X-PRO-Auth-Payload", this.encoder.Encode(payload, this.appSecret));
    IRestResponse response = this.restClient.Execute(request);
    if (response.IsSuccessful)
    {
        return JsonConvert.DeserializeObject<List<DocType>>(response.Content);
    }

    throw new Exception(response);
}
```

Eso es todo. Repita esto cada vez que necesite invocar una operación en el servicio.

```csharp
IEvertecAPIService client = new EvertecAPIService(new HardCodedCredentials());
client.Signin();
IList<DocType> docTypes = client.GetDocTypes();
```
