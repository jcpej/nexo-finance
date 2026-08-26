# Nexo Finance — GitHub Edition v8

Esta edição foi criada para funcionar **sem VPS, sem Node.js e sem banco de dados externo**. Pode ser publicada diretamente no **GitHub Pages**.

## O que mudou

- `index.html` é totalmente estático e funciona no GitHub Pages.
- Ao criar uma conta pública, o navegador gera e baixa automaticamente `nexo-conta-USUARIO.nexo`.
- O arquivo `.nexo` contém a conta e os dados financeiros criptografados.
- Criptografia: **PBKDF2-SHA-256 (210.000 iterações) + AES-GCM 256 bits** via Web Crypto API.
- O arquivo pode ser importado na própria tela de login em outro navegador/computador/celular.
- Em **Minha conta**, existe o botão **Baixar arquivo-cofre atualizado**.
- Ao trocar a senha, um novo arquivo-cofre é gerado automaticamente.
- Arquivos portáteis nunca restauram privilégios de administrador: a importação força o papel `member`.
- O cadastro público global é definido pelo arquivo `site-config.js`.

## Limitação inevitável do GitHub Pages

GitHub Pages é hospedagem estática. Um visitante do site **não pode gravar automaticamente um arquivo novo dentro do repositório**.

Fazer isso exigiria uma credencial do GitHub com permissão de escrita. Colocar essa credencial dentro do JavaScript público seria inseguro: qualquer visitante conseguiria extraí-la e escrever/apagar conteúdo do repositório.

Por isso, nesta edição:

1. A conta fica no navegador em que foi criada.
2. Uma cópia portátil criptografada é baixada para o usuário.
3. Em outro dispositivo, o usuário restaura a conta usando o arquivo `.nexo` + senha.
4. O GitHub hospeda **o aplicativo**, não os dados privados das contas.

Consequência: contas criadas em computadores diferentes **não aparecem automaticamente no painel do administrador**. Mensagens e visão consolidada do admin também são locais ao navegador. Para sincronização central em tempo real é necessário algum serviço de backend/banco, ainda que gratuito.

## Como publicar no GitHub Pages

1. Crie uma conta no GitHub, caso ainda não tenha.
2. Crie um repositório novo. Exemplo: `nexo-finance`.
3. Envie para a raiz do repositório estes arquivos:
   - `index.html`
   - `site-config.js`
   - `.nojekyll`
4. Abra **Settings** do repositório.
5. Entre em **Pages**.
6. Em **Build and deployment > Source**, escolha **Deploy from a branch**.
7. Escolha a branch **main** e a pasta **/(root)**.
8. Clique em **Save**.
9. Quando o GitHub terminar a publicação, a própria página de Settings > Pages mostrará o endereço do site.

## Abrir ou fechar o cadastro para todos

O arquivo `site-config.js` contém:

```js
publicRegistration: true
```

- `true` = cadastro aberto.
- `false` = cadastro fechado.

No painel administrativo, o comando de cadastro gera automaticamente um novo `site-config.js` quando você muda a chave. Depois, substitua o arquivo no repositório GitHub.

Essa substituição manual é necessária porque o site público não recebe credenciais de escrita do GitHub.

## Arquivo-cofre `.nexo`

### Criação
Ao concluir um cadastro público, o download é disparado automaticamente.

### Restaurar em outro dispositivo
1. Abra o Nexo Finance.
2. Clique em **Abrir meu arquivo de conta**.
3. Selecione o `.nexo`.
4. Digite a senha da conta.
5. A conta e os dados contidos naquela cópia serão restaurados no navegador.

### Manter o cofre atualizado
Depois de lançar novas movimentações, investimentos, metas etc., entre em **Minha conta > Baixar arquivo-cofre atualizado**.

O navegador não consegue alterar automaticamente um arquivo que já está na pasta Downloads de forma universal, especialmente em iPhone/Safari. Por isso é gerada uma nova cópia quando solicitado.

## Segurança

- Não envie arquivos `.nexo` para o repositório GitHub.
- Não coloque extratos, backups ou arquivos JSON de usuários no repositório.
- O repositório do GitHub Pages deve conter somente os arquivos públicos do aplicativo.
- Use uma senha forte para o arquivo-cofre.
- Guarde pelo menos uma cópia do `.nexo` em local confiável.

## Arquivos

- `index.html` — aplicativo.
- `site-config.js` — abre/fecha cadastro público global no site estático.
- `.nojekyll` — impede processamento desnecessário pelo Jekyll.
- `LEIA-ME.md` — este guia.
