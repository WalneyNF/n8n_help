# 📌 Guia de Manipulação de Dados no n8n

Este documento reúne funções essenciais para manipulação de dados dentro do **n8n**, incluindo formatação de **telefones, documentos (CPF, CNPJ, RG, Inscrição Estadual), remoção de acentos, JSON, datas** e outras transformações importantes.  

💡 **Objetivo:** Ajudar desenvolvedores e automação de processos a lidar com dados de forma eficiente e prática no n8n.  

🔗 **Como usar?** Basta copiar e colar as funções no nó "Set" ou "Function" do n8n, ajustando conforme sua necessidade.  

## 📌 Funções

### `$json.const.length()`
Obtém o comprimento (quantidade de caracteres) do valor armazenado em `$json.const`.
Se `const` for uma string "teste", então `$json.const.length()` retorna 5.

### `parseInt($json.const.length())`
Converte o comprimento da string para um número inteiro.
Isso pode ser útil para garantir que o valor seja tratado como número.

## 📌 Outras funções úteis no n8n

Aqui estão algumas funções comuns e seus usos:

### 1. Manipulação de Strings

```js
{{ $json.nome.toUpperCase() }}  // Converte para maiúsculas
{{ $json.nome.toLowerCase() }}  // Converte para minúsculas
{{ $json.nome.replace(" ", "-") }}  // Substitui espaço por hífen
{{ $json.nome.substring(0, 5) }}  // Pega os primeiros 5 caracteres

Exemplo: Se $json.nome = "Nova Friburgo", então:

toUpperCase() → "NOVA FRIBURGO"
toLowerCase() → "nova friburgo"
replace(" ", "-") → "Nova-Friburgo"

2. Números e Cálculos
{{ parseInt($json.idade) + 5 }}  // Soma 5 à idade
{{ $json.preco.toFixed(2) }}  // Formata número com duas casas decimais
{{ Math.round($json.preco) }}  // Arredonda número
{{ Math.random() }}  // Gera um número aleatório entre 0 e 1

Exemplo: Se $json.preco = 10.756, então:

toFixed(2) → "10.76"
Math.round(10.756) → 11

3. Datas e Horários
{{ new Date().toISOString() }}  // Data atual no formato ISO
{{ new Date().toLocaleString() }}  // Data e hora no formato local
{{ new Date($json.data).getFullYear() }}  // Retorna o ano de uma data
{{ new Date().getTime() }}  // Timestamp (milissegundos desde 1970)

Exemplo: Se $json.data = "2024-02-06T10:00:00Z", então:

getFullYear() → 2024

4. JSON e Arrays
{{ JSON.stringify($json) }}  // Converte objeto para string JSON
{{ JSON.parse($json.texto) }}  // Converte string JSON para objeto
{{ $json.lista.length }}  // Conta quantos itens existem em um array
{{ $json.lista.includes("item1") }}  // Verifica se um item está no array
{{ $json.lista.join(", ") }}  // Junta elementos do array em uma string

Exemplo: Se $json.lista = ["RJ", "SP", "MG"], então:

join(", ") → "RJ, SP, MG"

📌 Exemplo prático no n8n
Objetivo: Criar um link IBGE formatado a partir dos dados do ViaCEP

{{ "https://cidades.ibge.gov.br/brasil/" + $json.uf.toLowerCase() + "/" + $json.localidade.toLowerCase().replace(/\s+/g, '-') + "/panorama" }}

Se $json.localidade = "Nova Friburgo" e $json.uf = "RJ", o resultado será:

https://cidades.ibge.gov.br/brasil/rj/nova-friburgo/panorama

Essas funções ajudam a transformar dados no n8n sem precisar de um nó de código! Quer mais algum exemplo? 😊

📌 Tabela de Funções Úteis no n8n

🔤 Strings
{{ $json.nome.toUpperCase() }}	Converte para maiúsculas	"nova friburgo" → "NOVA FRIBURGO"
{{ $json.nome.toLowerCase() }}	Converte para minúsculas	"Nova Friburgo" → "nova friburgo"
{{ $json.nome.replace(" ", "-") }}	Substitui espaços por hífens	"Nova Friburgo" → "Nova-Friburgo"
{{ $json.nome.substring(0, 5) }}	Pega os 5 primeiros caracteres	"Friburgo" → "Fribu"
{{ $json.nome.includes("Friburgo") }}	Verifica se contém um termo específico	"Nova Friburgo" → true
{{ $json.nome.split(" ") }}	Divide uma string em um array	"Nova Friburgo" → ["Nova", "Friburgo"]
{{ $json.nome.trim() }}	Remove espaços extras no início e fim	" Nova Friburgo " → "Nova Friburgo"

🔢 Números
{{ parseInt($json.idade) }}	Converte para inteiro	"47" → 47
{{ parseFloat($json.preco).toFixed(2) }}	Formata número com duas casas decimais	10.756 → "10.76"
{{ Math.round($json.preco) }}	Arredonda para o número inteiro mais próximo	10.6 → 11
{{ Math.ceil($json.preco) }}	Arredonda para cima	10.3 → 11
{{ Math.floor($json.preco) }}	Arredonda para baixo	10.9 → 10
{{ Math.random() }}	Gera um número aleatório entre 0 e 1	Exemplo: 0.7362

📅 Datas e Horários
{{ new Date().toISOString() }}	Retorna data e hora atuais no formato ISO	"2025-02-06T14:30:00.000Z"
{{ new Date().toLocaleString() }}	Data e hora no formato local	"06/02/2025, 11:30:00"
{{ new Date().getFullYear() }}	Retorna o ano atual	2025
{{ new Date().getTime() }}	Retorna o timestamp (milissegundos desde 1970)	1707222000000
{{ new Date($json.data).toDateString() }}	Converte data para formato legível	"Wed Feb 06 2025"

📦 JSON / Objetos
{{ JSON.stringify($json) }}	Converte objeto para string JSON	{ "cidade": "Nova Friburgo" } → "{\"cidade\":\"Nova Friburgo\"}"
{{ JSON.parse($json.texto) }}	Converte string JSON para objeto	"{"cidade":"Nova Friburgo"}" → { "cidade": "Nova Friburgo" }
{{ Object.keys($json) }}	Retorna um array com as chaves do objeto	{ "cep": "28623-680", "uf": "RJ" } → ["cep", "uf"]
{{ Object.values($json) }}	Retorna um array com os valores do objeto	{ "cep": "28623-680", "uf": "RJ" } → ["28623-680", "RJ"]
🗂 Arrays / Listas	{{ $json.lista.length }}	Conta quantos itens existem no array	["RJ", "SP", "MG"] → 3
{{ $json.lista.includes("RJ") }}	Verifica se um item está no array	["RJ", "SP", "MG"] → true
{{ $json.lista.join(", ") }}	Junta os elementos do array em uma string separada por vírgula	["RJ", "SP", "MG"] → "RJ, SP, MG"
{{ $json.lista.map(item => item.toUpperCase()) }}	Converte cada item do array para maiúscula	["rj", "sp", "mg"] → ["RJ", "SP", "MG"]
{{ $json.lista.sort() }}	Ordena os elementos do array	["MG", "SP", "RJ"] → ["MG", "RJ", "SP"]

💡 Dica: Teste as funções no ambiente de desenvolvimento do n8n para verificar se estão funcionando conforme esperado!

---

## 🤝 Contribuições

Se você tiver sugestões, melhorias ou quiser adicionar mais funções úteis, sinta-se à vontade para contribuir!  

💬 **Dúvidas ou sugestões?**  
Abra uma issue ou entre em contato!  

🌎 **Compartilhe este guia!**  
Se este documento te ajudou, considere compartilhar com a comunidade de automação no n8n.  

🚀 **Feito para facilitar suas automações!**  

Atenciosamente
Walney Moreira Klein - walneyk@hotmail.com
Documento teve ajuda do ChatGPT
Data: Nova Friburgo-RJ- 06/02/2025

