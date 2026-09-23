# Entrar no servidor · Olympo

A página que o botão do Discord abre. Ela recebe a arena pela URL
(`?arena=firegames2`), entrega ao Steam (`steam://connect/host:porta`) e
o CS2 abre já conectando.

Ela existe porque o **Discord recusa `steam://` em botão de link**
(medido em 22/09/2026: `URL_TYPE_INVALID_SCHEME: Scheme must be one of
('http', 'https', 'discord')`). Um endereço `https` no meio do caminho é
o que transforma o clique em entrada no jogo.

## Não é um redirecionador aberto

A página **não** aceita endereço pela URL: ela carrega o mapa das arenas
dentro dela, e a URL só escolhe uma pela chave. Se aceitasse `?ip=`,
qualquer pessoa montaria um link com a nossa cara mandando a sala para o
servidor dela.

## O endereço mora em um lugar só

`index.html` é **gerado** — não se edita à mão. Ele sai da mesma
configuração que o `!ip` e o botão do Discord leem. A partir de
`C:/Projetos/montes/backend`:

    python -m montes.infrastructure.pagina_de_entrar escreve C:/Projetos/olympo-entrar
    python -m montes.infrastructure.pagina_de_entrar confere <url-publicada>

O `confere` baixa o que está no ar e compara com a configuração de hoje.
É a guarda contra o pior defeito daqui: o servidor muda de porta, o `!ip`
passa a dizer o novo, e esta página continua levando a sala para o
velho — sem erro, sem aviso.
