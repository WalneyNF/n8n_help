# 📌 Guia de Manipulação de Dados no n8n

Este documento reúne funções essenciais para manipulação de dados dentro do **n8n**, incluindo formatação de **telefones, documentos (CPF, CNPJ, RG, Inscrição Estadual), remoção de acentos, JSON, datas** e outras transformações importantes.  

💡 **Objetivo:** Ajudar desenvolvedores e automação de processos a lidar com dados de forma eficiente e prática no n8n.  

🔗 **Como usar?** Basta copiar e colar as funções no nó "Set" ou "Function" do n8n, ajustando conforme sua necessidade.  


📌 Funções 
$json.const.length()

Obtém o comprimento (quantidade de caracteres) do valor armazenado em $json.const.
Se const for uma string "teste", então $json.const.length() retorna 5.
parseInt($json.const.length())

Converte o comprimento da string para um número inteiro.
Isso pode ser útil para garantir que o valor seja tratado como número.
📌 Outras funções úteis no n8n
Aqui estão algumas funções comuns e seus usos:

1. Manipulação de Strings

{{ $json.nome.toUpperCase() }}  // Converte para maiúsculas
{{ $json.nome.toLowerCase() }}  // Converte para minúsculas
{{ $json.nome.replace(" ", "-") }}  // Substitui espaço por hífen
{{ $json.nome.substring(0, 5) }}  // Pega os primeiros 5 caracteres
Exemplo:
Se $json.nome = "Nova Friburgo", então:

toUpperCase() → "NOVA FRIBURGO"
toLowerCase() → "nova friburgo"
replace(" ", "-") → "Nova-Friburgo"

2. Números e Cálculos

{{ parseInt($json.idade) + 5 }}  // Soma 5 à idade
{{ $json.preco.toFixed(2) }}  // Formata número com duas casas decimais
{{ Math.round($json.preco) }}  // Arredonda número
{{ Math.random() }}  // Gera um número aleatório entre 0 e 1
Exemplo:
Se $json.preco = 10.756, então:

toFixed(2) → "10.76"
Math.round(10.756) → 11

3. Datas e Horários

{{ new Date().toISOString() }}  // Data atual no formato ISO
{{ new Date().toLocaleString() }}  // Data e hora no formato local
{{ new Date($json.data).getFullYear() }}  // Retorna o ano de uma data
{{ new Date().getTime() }}  // Timestamp (milissegundos desde 1970)
Exemplo:
Se $json.data = "2024-02-06T10:00:00Z", então:

getFullYear() → 2024

4. JSON e Arrays

{{ JSON.stringify($json) }}  // Converte objeto para string JSON
{{ JSON.parse($json.texto) }}  // Converte string JSON para objeto
{{ $json.lista.length }}  // Conta quantos itens existem em um array
{{ $json.lista.includes("item1") }}  // Verifica se um item está no array
{{ $json.lista.join(", ") }}  // Junta elementos do array em uma string
Exemplo:
Se $json.lista = ["RJ", "SP", "MG"], então:

join(", ") → "RJ, SP, MG"

📌 Exemplo prático no n8n
Objetivo: Criar um link IBGE formatado a partir dos dados do ViaCEP

{{ "https://cidades.ibge.gov.br/brasil/" + $json.uf.toLowerCase() + "/" + $json.localidade.toLowerCase().replace(/\s+/g, '-') + "/panorama" }}
Se $json.localidade = "Nova Friburgo" e $json.uf = "RJ", o resultado será:

https://cidades.ibge.gov.br/brasil/rj/nova-friburgo/panorama
Essas funções ajudam a transformar dados no n8n sem precisar de um nó de código! Quer mais algum exemplo? 😊

Aqui está uma tabela com funções úteis para o n8n, organizadas por categorias. Essas funções ajudam a manipular strings, números, datas, JSON e arrays dentro dos workflows.

📌 Tabela de Funções Úteis no n8n
Categoria	Função	Descrição / Uso	Exemplo / Saída

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
{{ JSON.parse($json.texto) }}	Converte string JSON para objeto	"{\"cidade\":\"Nova Friburgo\"}" → { "cidade": "Nova Friburgo" }
{{ Object.keys($json) }}	Retorna um array com as chaves do objeto	{ "cep": "28623-680", "uf": "RJ" } → ["cep", "uf"]
{{ Object.values($json) }}	Retorna um array com os valores do objeto	{ "cep": "28623-680", "uf": "RJ" } → ["28623-680", "RJ"]

🗂 Arrays / Listas	

{{ $json.lista.length }}	Conta quantos itens existem no array	["RJ", "SP", "MG"] → 3
{{ $json.lista.includes("RJ") }}	Verifica se um item está no array	["RJ", "SP", "MG"] → true
{{ $json.lista.join(", ") }}	Junta os elementos do array em uma string separada por vírgula	["RJ", "SP", "MG"] → "RJ, SP, MG"
{{ $json.lista.map(item => item.toUpperCase()) }}	Converte cada item do array para maiúscula	["rj", "sp", "mg"] → ["RJ", "SP", "MG"]
{{ $json.lista.filter(item => item !== "RJ") }}	Remove um item específico do array	["RJ", "SP", "MG"] → ["SP", "MG"]
{{ $json.lista.reverse() }}	Inverte a ordem dos itens do array	["RJ", "SP", "MG"] → ["MG", "SP", "RJ"]

📌 Exemplo prático no n8n

{{ "https://cidades.ibge.gov.br/brasil/" + $json.uf.toLowerCase() + "/" + $json.localidade.toLowerCase().replace(/\s+/g, '-') + "/panorama" }}
Entrada ($json):

{
  "localidade": "Nova Friburgo",
  "uf": "RJ"
}
Saída esperada:

https://cidades.ibge.gov.br/brasil/rj/nova-friburgo/panorama

📌 Resumo
Strings: Manipulação de textos (maiúsculas, substituições, recortes).
Números: Conversão, arredondamento e cálculos.
Datas: Formatação e obtenção de tempo.
JSON: Conversão e extração de valores.
Arrays: Contagem, busca, manipulação e filtragem.


🚀 Aqui vai mais um conjunto de funções úteis para n8n, incluindo manipulação de strings avançada, arrays, datas, objetos e expressões regulares. Vou adicionar mais exemplos que podem ser úteis no seu workflow!

📌 Mais Funções Úteis para n8n

Categoria	Função	Descrição / Uso	Exemplo / Saída

🔤 Strings Avançadas	

{{ $json.texto.startsWith("Nova") }}	Verifica se começa com determinado valor	"Nova Friburgo" → true
{{ $json.texto.endsWith("Friburgo") }}	Verifica se termina com determinado valor	"Nova Friburgo" → true
{{ $json.texto.charAt(0) }}	Retorna o primeiro caractere	"Friburgo" → "F"
{{ $json.texto.slice(0, 4) }}	Corta a string entre os índices 0 e 4	"Friburgo" → "Frib"
{{ $json.texto.replace(/\d+/g, '') }}	Remove números de uma string usando Regex	"Rua 123 Araguaia" → "Rua Araguaia"

🔢 Números Avançados

{{ Math.min(...$json.numeros) }}	Retorna o menor número de um array	[10, 5, 8] → 5
{{ Math.max(...$json.numeros) }}	Retorna o maior número de um array	[10, 5, 8] → 10
{{ (parseFloat($json.preco) * 1.1).toFixed(2) }}	Calcula 10% de aumento e formata com 2 casas decimais	100 → "110.00"

📅 Datas Avançadas	

{{ new Date().getDay() }}	Retorna o dia da semana (0 = Domingo, 1 = Segunda...)	0
{{ new Date().getMonth() + 1 }}	Retorna o mês (Janeiro = 1, Fevereiro = 2...)	2
{{ new Date(new Date().setDate(new Date().getDate() + 7)).toDateString() }}	Adiciona 7 dias à data atual	"Wed Feb 13 2025"

📦 Manipulação de JSON	

{{ JSON.stringify($json, null, 2) }}	Converte objeto JSON para string formatada (legível)	{ "uf": "RJ" } → "{"uf": "RJ"}"
{{ $json.hasOwnProperty("uf") }}	Verifica se um campo existe no JSON	{ "uf": "RJ" } → true

🗂 Arrays Avançados	

{{ $json.lista.find(item => item === "SP") }}	Retorna o primeiro item encontrado	["RJ", "SP", "MG"] → "SP"
{{ $json.lista.map(item => item.length) }}	Retorna um array com os tamanhos dos itens	["RJ", "SP", "MG"] → [2, 2, 2]
{{ $json.lista.every(item => item.length === 2) }}	Verifica se todos os itens têm 2 caracteres	["RJ", "SP", "MG"] → true
{{ $json.lista.some(item => item === "RJ") }}	Verifica se existe pelo menos um "RJ" no array	["RJ", "SP", "MG"] → true
{{ $json.lista.sort() }}	Ordena um array em ordem alfabética	["Friburgo", "Nova"] → ["Friburgo", "Nova"]

🔍 Expressões Regulares (Regex)	

{{ $json.texto.match(/\d+/g) }}	Retorna apenas os números de uma string	"Rua 123" → ["123"]
{{ $json.texto.replace(/\s+/g, "-") }}	Substitui espaços por hífens	"Nova Friburgo" → "Nova-Friburgo"
{{ $json.texto.match(/[A-Z]/g) }}	Retorna todas as letras maiúsculas da string	"Nova Friburgo RJ" → ["N", "F", "R", "J"]

📌 Mais exemplos práticos no n8n

1️⃣ Criando um link formatado para o IBGE

{{ "https://cidades.ibge.gov.br/brasil/" + $json.uf.toLowerCase() + "/" + $json.localidade.toLowerCase().replace(/\s+/g, '-') + "/panorama" }}
Entrada ($json):

{
  "localidade": "Nova Friburgo",
  "uf": "RJ"
}

https://cidades.ibge.gov.br/brasil/rj/nova-friburgo/panorama

2️⃣ Filtrando apenas números do endereço

{{ $json.endereco.match(/\d+/g) }}
Entrada ($json):

{
  "endereco": "Rua 123 Araguaia, 45"
}
Saída esperada:

["123", "45"]

3️⃣ Somando todos os valores de um array numérico

{{ $json.valores.reduce((acc, val) => acc + val, 0) }}
Entrada ($json):

{
  "valores": [10, 20, 30]
}
Saída esperada:


4️⃣ Ordenando uma lista de cidades

{{ $json.cidades.sort() }}
Entrada ($json):

{
  "cidades": ["Friburgo", "Teresópolis", "Petrópolis"]
}
Saída esperada:

["Friburgo", "Petrópolis", "Teresópolis"]

📌 Resumo das novas funções
Strings Avançadas: Detectar início/fim, remover números, capturar caracteres.
Números Avançados: Encontrar maior/menor, calcular valores.
Datas Avançadas: Pegar mês/dia, somar dias, transformar timestamps.
Manipulação de JSON: Stringify, verificar chaves.
Arrays Avançados: Ordenação, buscas, verificação de existência.
Regex: Extração e substituição de padrões.
Agora você tem um super kit de funções para o n8n! 🔥 Se precisar de mais algo específico, só perguntar! 🚀

📌 Mais Funções Avançadas para n8n
Categoria	Função	Descrição / Uso	Exemplo / Saída

🔤 Strings Extras

{{ $json.texto.toUpperCase() }}	Converte tudo para maiúsculas	"friburgo" → "FRIBURGO"
{{ $json.texto.toLowerCase() }}	Converte tudo para minúsculas	"Friburgo" → "friburgo"
{{ $json.texto.trim() }}	Remove espaços extras no início e fim da string	" Friburgo " → "Friburgo"
{{ encodeURI($json.texto) }}	Converte para URL encode	"Nova Friburgo" → "Nova%20Friburgo"
{{ decodeURI($json.texto) }}	Converte URL encode para texto normal	"Nova%20Friburgo" → "Nova Friburgo"

🔢 Números Extras

{{ Math.round($json.valor) }}	Arredonda para o número inteiro mais próximo	10.7 → 11
{{ Math.floor($json.valor) }}	Arredonda para baixo	10.9 → 10
{{ Math.ceil($json.valor) }}	Arredonda para cima	10.1 → 11
{{ Math.abs($json.valor) }}	Retorna o valor absoluto	-10 → 10

📅 Datas Extras

{{ new Date().toISOString() }}	Retorna a data atual no formato ISO 8601	"2025-02-06T12:00:00.000Z"
{{ new Date().toLocaleDateString("pt-BR") }}	Formata a data para pt-BR	"06/02/2025"
{{ new Date().toLocaleTimeString("pt-BR") }}	Retorna apenas a hora formatada	"12:00:00"
{{ Date.now() }}	Retorna o timestamp atual	1707206400000
{{ new Date($json.data).getFullYear() }}	Extrai o ano de uma data	"2025-02-06" → 2025

📦 Manipulação de JSON Avançada

{{ Object.keys($json) }}	Retorna todas as chaves do JSON	{ "uf": "RJ", "cidade": "Nova Friburgo" } → ["uf", "cidade"]
{{ Object.values($json) }}	Retorna todos os valores do JSON	{ "uf": "RJ", "cidade": "Nova Friburgo" } → ["RJ", "Nova Friburgo"]
{{ Object.entries($json) }}	Retorna um array de chave-valor	{ "uf": "RJ", "cidade": "Nova Friburgo" } → [["uf", "RJ"], ["cidade", "Nova Friburgo"]]

🗂 Arrays Extras

{{ $json.lista.includes("RJ") }}	Verifica se o array contém "RJ"	["RJ", "SP", "MG"] → true
{{ $json.lista.reverse() }}	Inverte a ordem do array	["RJ", "SP", "MG"] → ["MG", "SP", "RJ"]
{{ $json.lista.join(", ") }}	Converte um array em string separada por vírgula	["RJ", "SP", "MG"] → "RJ, SP, MG"
{{ Array.isArray($json.lista) }}	Verifica se é um array	["RJ", "SP"] → true
{{ $json.lista.filter(item => item !== "RJ") }}	Remove "RJ" do array	["RJ", "SP", "MG"] → ["SP", "MG"]

🔍 Regex Avançado
{{ /[A-Z]/.test($json.texto) }}	Verifica se há letras maiúsculas	"friburgo" → false
{{ $json.texto.replace(/\d+/g, "***") }}	Substitui todos os números por "*"**	"Rua 123" → "Rua ***"
{{ $json.texto.match(/\b\w{5}\b/g) }}	Retorna palavras com exatamente 5 letras	"Friburgo Nova Rio" → ["Nova"]

📌 Exemplos práticos no n8n

1️⃣ Criando um Link de Pesquisa no Google

{{ "https://www.google.com/search?q=" + encodeURIComponent($json.termo) }}
Entrada ($json):

{
  "termo": "melhores softwares para MEI"
}
Saída esperada:

https://www.google.com/search?q=melhores%20softwares%20para%20MEI

2️⃣ Filtrando um JSON para obter apenas cidades do RJ

{{ $json.cidades.filter(cidade => cidade.uf === "RJ") }}
Entrada ($json):

{
  "cidades": [
    { "nome": "Nova Friburgo", "uf": "RJ" },
    { "nome": "São Paulo", "uf": "SP" }
  ]
}
Saída esperada:

[
  { "nome": "Nova Friburgo", "uf": "RJ" }
]

3️⃣ Convertendo um JSON em string formatada

{{ JSON.stringify($json, null, 2) }}
Entrada ($json):

{
  "cidade": "Nova Friburgo",
  "uf": "RJ"
}
Saída esperada:

{
  "cidade": "Nova Friburgo",
  "uf": "RJ"
}

4️⃣ Verificando se um e-mail é válido

{{ /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/.test($json.email) }}
Entrada ($json):

{
  "email": "teste@email.com"
}
Saída esperada:


📌 Resumo das novas funções
Strings Extras: Maiúsculas, minúsculas, trim, encode URI.
Números Extras: Arredondamentos, valor absoluto.
Datas Extras: ISO date, timestamp, conversões de data/hora.
Manipulação de JSON: Obter chaves, valores, entradas.
Arrays Extras: Verificação, inversão, filtragem.
Regex Avançado: Busca de padrões mais complexos.

📌 Funções Avançadas para Manipulação de Dados no n8n

📞 Telefones

{{ $json.telefone.replace(/\D/g, "") }}	Remove todos os caracteres não numéricos	"(22) 99999-1234" → "22999991234"
{{ $json.telefone.replace(/\D/g, "").slice(-8) }}	Retorna apenas os 8 últimos dígitos do telefone	"(22) 99999-1234" → "99991234"
{{ $json.telefone.replace(/\D/g, "").replace(/^(\d{2})(\d{5})(\d{4})$/, "($1) $2-$3") }}	Formata telefone com DDD e hífen	"22999991234" → "(22) 99999-1234"

🆔 Documentos (CPF, CNPJ, RG)

{{ $json.cpf.replace(/\D/g, "") }}	Remove pontos e traço do CPF	"123.456.789-09" → "12345678909"
{{ $json.cnpj.replace(/\D/g, "") }}	Remove pontos, barras e traços do CNPJ	"12.345.678/0001-99" → "12345678000199"
{{ $json.cpf.replace(/\D/g, "").replace(/^(\d{3})(\d{3})(\d{3})(\d{2})$/, "$1.$2.$3-$4") }}	Formata um CPF corretamente	"12345678909" → "123.456.789-09"
{{ $json.cnpj.replace(/\D/g, "").replace(/^(\d{2})(\d{3})(\d{3})(\d{4})(\d{2})$/, "$1.$2.$3/$4-$5") }}	Formata um CNPJ corretamente	"12345678000199" → "12.345.678/0001-99"
{{ $json.rg.replace(/\D/g, "") }}	Remove traços e pontos do RG	"12.345.678-9" → "123456789"
{{ $json.inscricaoEstadual.replace(/\D/g, "") }}	Remove formatos da Inscrição Estadual	"123.456.789.012" → "123456789012"

🔤 Remoção de Acentos

{{ $json.texto.normalize("NFD").replace(/[\u0300-\u036f]/g, "") }}	Remove acentos de palavras	"São João" → "Sao Joao"
{{ $json.texto.replace(/[áàãâä]/g, "a").replace(/[éèêë]/g, "e").replace(/[íìîï]/g, "i").replace(/[óòõôö]/g, "o").replace(/[úùûü]/g, "u").replace(/[ç]/g, "c") }}	Alternativa manual de remoção de acentos	"açaí, café, cachaça" → "acai, cafe, cachaca"

🔤 Textos & Caracteres Especiais

{{ $json.texto.replace(/[^a-zA-Z0-9 ]/g, "") }}	Remove todos os caracteres especiais	"Nova Friburgo @ 100%" → "Nova Friburgo 100"
{{ $json.texto.replace(/\s+/g, " ") }}	Substitui espaços extras por um único espaço	" Nova Friburgo " → "Nova Friburgo"
{{ $json.texto.replace(/\b\w/g, letra => letra.toUpperCase()) }}	Primeira letra de cada palavra em maiúsculo	"nova friburgo" → "Nova Friburgo"

📆 Datas & Horários Extras

{{ new Date($json.data).toLocaleDateString("pt-BR") }}	Formata uma data para o padrão brasileiro	"2025-02-06" → "06/02/2025"
{{ new Date().toISOString().slice(0,10) }}	Retorna apenas a data atual no formato ISO	"2025-02-06"
{{ new Date($json.data).getFullYear() }}	Extrai apenas o ano de uma data	"2025-02-06" → 2025
{{ new Date($json.data).getMonth() + 1 }}	Extrai apenas o mês (1-12)	"2025-02-06" → 2
{{ new Date($json.data).getDate() }}	Extrai apenas o dia do mês	"2025-02-06" → 6

📌 Exemplos Práticos no n8n

1️⃣ Normalizando e Formatando Telefones

{{ $json.telefone.replace(/\D/g, "").replace(/^(\d{2})(\d{5})(\d{4})$/, "($1) $2-$3") }}
🔹 Entrada ($json):

{
  "telefone": "(22) 99999-1234"
}
🔹 Saída esperada:

"(22) 99999-1234"

2️⃣ Validando e Formatando um CPF

{{ $json.cpf.replace(/\D/g, "").replace(/^(\d{3})(\d{3})(\d{3})(\d{2})$/, "$1.$2.$3-$4") }}
🔹 Entrada ($json):

{
  "cpf": "123.456.789-09"
}
🔹 Saída esperada:

"123.456.789-09"
3️⃣ Removendo Acentos e Caracteres Especiais

{{ $json.texto.normalize("NFD").replace(/[\u0300-\u036f]/g, "").replace(/[^a-zA-Z0-9 ]/g, "") }}
🔹 Entrada ($json):

{
  "texto": "São João & Café 100%"
}
🔹 Saída esperada:

"Sao Joao Cafe 100"

4️⃣ Formatando uma Data para o Padrão Brasileiro

{{ new Date($json.data).toLocaleDateString("pt-BR") }}
🔹 Entrada ($json):

{
  "data": "2025-02-06T12:00:00Z"
}
🔹 Saída esperada:

📌 Resumo das Novas Funções
✅ Telefones: Remover caracteres especiais, formatar com DDD e hífen
✅ Documentos: CPF, CNPJ, RG, Inscrição Estadual – formatação e limpeza
✅ Acentos & Caracteres: Remover acentos, caracteres especiais, normalizar textos
✅ Datas: Formatar para o padrão BR, extrair dia/mês/ano

📌 Funções Essenciais para Manipulação de Dados no n8n
Este documento contém uma lista de funções essenciais para trabalhar com telefones, documentos (CPF, CNPJ, RG), remoção de acentos, formatação de textos e datas no n8n.

📞 Telefones

{{ $json.telefone.replace(/\D/g, "") }}	Remove caracteres não numéricos	"(22) 99999-1234" ➝ "22999991234"
{{ $json.telefone.replace(/\D/g, "").replace(/^(\d{2})(\d{5})(\d{4})$/, "($1) $2-$3") }}	Formata telefone com DDD e hífen	"22999991234" ➝ "(22) 99999-1234"

🆔 Documentos (CPF, CNPJ, RG)

{{ $json.cpf.replace(/\D/g, "") }}	Remove formatação do CPF	"123.456.789-09" ➝ "12345678909"
{{ $json.cpf.replace(/\D/g, "").replace(/^(\d{3})(\d{3})(\d{3})(\d{2})$/, "$1.$2.$3-$4") }}	Formata um CPF	"12345678909" ➝ "123.456.789-09"
{{ $json.cnpj.replace(/\D/g, "") }}	Remove formatação do CNPJ	"12.345.678/0001-99" ➝ "12345678000199"
{{ $json.cnpj.replace(/\D/g, "").replace(/^(\d{2})(\d{3})(\d{3})(\d{4})(\d{2})$/, "$1.$2.$3/$4-$5") }}	Formata um CNPJ	"12345678000199" ➝ "12.345.678/0001-99"

🔤 Remoção de Acentos

{{ $json.texto.normalize("NFD").replace(/[\u0300-\u036f]/g, "") }}	Remove acentos	"São João" ➝ "Sao Joao"
{{ $json.texto.replace(/[^a-zA-Z0-9 ]/g, "") }}	Remove caracteres especiais	"Nova Friburgo @ 100%" ➝ "Nova Friburgo 100"

📆 Datas

{{ new Date($json.data).toLocaleDateString("pt-BR") }}	Formata data para padrão brasileiro	"2025-02-06" ➝ "06/02/2025"
{{ new Date().toISOString().slice(0,10) }}	Retorna a data atual em formato ISO	"2025-02-06"
{{ new Date($json.data).getFullYear() }}	Extrai apenas o ano	"2025-02-06" ➝ 2025
{{ new Date($json.data).getMonth() + 1 }}	Extrai apenas o mês	"2025-02-06" ➝ 2
{{ new Date($json.data).getDate() }}	Extrai apenas o dia	"2025-02-06" ➝ 6

🚀 Exemplo de Uso no n8n

1️⃣ Normalizando e Formatando Telefones

{{ $json.telefone.replace(/\D/g, "").replace(/^(\d{2})(\d{5})(\d{4})$/, "($1) $2-$3") }}
Entrada:

{
  "telefone": "(22) 99999-1234"
}

Saída esperada:

"(22) 99999-1234"

2️⃣ Formatando um CPF
{{ $json.cpf.replace(/\D/g, "").replace(/^(\d{3})(\d{3})(\d{3})(\d{2})$/, "$1.$2.$3-$4") }}

Entrada:

{
  "cpf": "12345678909"
}

Saída esperada:

"123.456.789-09"

Essas funções são úteis para manipular e normalizar dados no n8n de forma eficiente. Se precisar de mais alguma função, contribuições são bem-vindas! 🚀


---

## 🤝 Contribuições

Se você tiver sugestões, melhorias ou quiser adicionar mais funções úteis, sinta-se à vontade para contribuir!  

💬 **Dúvidas ou sugestões?**  
Abra uma issue ou entre em contato!  

🌎 **Compartilhe este guia!**  
Se este documento te ajudou, considere compartilhar com a comunidade de automação no n8n.  

🚀 **Feito para facilitar suas automações!**  

Atencisamente
Walney Moreira Klein - walneyk@hotmail.com
Com Ajuda do ChatGPT - 06/02/2025

