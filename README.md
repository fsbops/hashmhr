# hashmhr

**Verificador rápido de hashes contra o Malware Hash Registry (Team Cymru)**  
Função shell para checar MD5 / SHA1 / SHA256 via DNS queries.

---

## O que é
`hashmhr` detecta automaticamente o tipo do hash passado como argumento na chamada (MD5, SHA1 ou SHA256) e realiza a consulta apropriada ao Malware Hash Registry da Team Cymru, retornando um resumo legível com data da última análise e percentual de detecção (quando disponível).

---

## Uso

Coloque a função no seu `~/.bashrc`, `~/.zshrc` ou no seu arquico `.bash_aliases` na home do seu usuário. Abra um novo terminal e teste.
Função facilmente convertível em um script shell também.

---

## Forma de usar:

hashmhr <hash>

Exemplos:

hashmhr d41d8cd98f00b204e9800998ecf8427e
hashmhr da39a3ee5e6b4b0d3255bfef95601890afd80709
hashmhr 2d83c4d620866f4ae647ed6a70113686bb7b80b1a7bbdcf544fd0ffec105c4a6

---

## Saída esperada

MD5 / SHA1 (TXT query):
Se não encontrado: ✅ Hash não encontrado no Malware Hash Registry
Se encontrado: retorna epoch (convertido para data legível) e percentual de detecção.
📅 Última análise: 2025-10-21 14:22:03
⚠️  Detecção: 78%


SHA256 (query do tipo A):
se o retorno for 127.0.0.2 a hash é considerada maliciosa, e portanto, o retorno legível será:
"🔍 Tipo de hash detectado: SHA256
⚠️  Resultado: hash encontrado no Malware Hash Registry (malicioso)"
se o retorno for vazio (null) significa que não foi encontrado nenhum dado a respeito da hash e o retorno legível será algo como:
"🔍 Tipo de hash detectado: SHA256
✅ Hash não encontrado no Malware Hash Registry"

---

## Requisitos:
dig (do pacote bind9-dnsutils / dnsutils)
bash (funciona em shells compatíveis)
Conexão DNS funcional (resolução externa)

---

## Limitações e Segurança
O serviço do Team Cymru tem limites e políticas de uso; não faça varreduras massivas indiscriminadas.
Resultados dependem da base de dados pública — sempre valide com outras fontes se for um incidente crítico.
Não use em ambientes sensíveis sem autorização.

## Melhorias futuras:

--saida em json para um melhor aproveitamento e integração do recurso com plataformas diversas (chamada do script sob demanda e coleta do retorno, por exemplo)</br>
--suporte a leitura de um arquivo com vários hashes (modo batch)</br>
--verificação de conectividade DNS e fallback</br>
--integração com jq/curl para enriquecer com info de outras fontes/multiplas consultas e varias fontes</br>

## Licença
MIT — sinta-se livre para usar, modificar e distribuir.
