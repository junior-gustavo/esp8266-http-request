# Realizando requisições HTTP no ESP8266 utilizando a biblioteca HTTPClient

![img](https://raw.githubusercontent.com/douglaszuqueto/esp8266-http-request/master/files/esp8266-request.png)

## HTTP

### Verbos HTTP(mais utilizados - principalmente em API's)

* GET - requisitar registros do servidor
* POST - enviar algo para o servidor
* PUT - atualizar algum registro do servidor
* DELETE - remover algum registro do servidor

## Simples requisição

```c
// ############# HTTP REQUEST ################ //

void httpGet(String url)
{
  String payload = makeRequest(url);

  if (!payload) {
    return;
  }

  Serial.println("##[RESULT]## ==> " + payload);

}

String makeRequest(String url)
{
  http.begin(url);
  int httpCode = http.GET();

  if (httpCode < 0) {
    Serial.println("request error - " + httpCode);
    return "";

  }

  if (httpCode != HTTP_CODE_OK) {
    return "";
  }

  return http.getString();

  http.end();
}
```

## GET

```c
  http.begin(url);
  int httpCode = http.GET();
```

## POST

```c
  http.begin(url);
  http.addHeader("content-type", "application/x-www-form-urlencoded");

  String body = "id=7890&name=NTC&value=10";

  int httpCode = http.POST(body);
```

## Referências
