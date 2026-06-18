# rap-fnet-docs

Espelho **público** dos documentos da CVM / FundosNET (`fnet.bmfbovespa.com.br`),
já **decodificados** (o endpoint `exibirDocumento` devolve o arquivo em base64
dentro de um `text/plain`; aqui guardamos os bytes reais do PDF/HTML).

Serve de cache durável para o PWA **Rico aos Poucos**: o Cloudflare Worker
`fnet-doc` busca o documento aqui primeiro (via CDN) e só cai no FundosNET ao vivo
quando não encontra. Assim a abertura é instantânea e os timeouts do FNET somem.

Todo o conteúdo é **público da CVM** (documentos regulatórios de fundos listados).

## Layout

```
d/<2 últimos dígitos do id>/<id>
```

Exemplo: documento `id=1215320` → `d/20/1215320` (bytes crus; o Worker detecta
PDF vs HTML pelos magic bytes e serve com o Content-Type correto).

Populado automaticamente pelo pipeline do watcher FundosNET (droplet).
