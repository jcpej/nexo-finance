# Nexo Finance Cloud v9

Esta versão mantém o GitHub Pages como hospedagem da interface e usa Supabase como autoridade para contas e dados.

## Publicação no GitHub Pages

1. No repositório `jcpej/nexo-finance`, substitua o `index.html` atual pelo `index.html` desta pasta.
2. Mantenha `.nojekyll` na raiz. O antigo `site-config.js` pode permanecer, mas não é mais utilizado pela v9.
3. Aguarde o GitHub Pages concluir o deployment e abra `https://jcpej.github.io/nexo-finance/`.

## Primeira abertura

Enquanto ainda não existir administrador cloud, o site mostrará "Ativar administrador na nuvem".

- Usuário administrativo: `admin`
- Defina uma senha forte de no mínimo 12 caracteres.
- Informe o código de instalação fornecido pelo ChatGPT na conversa. Não coloque esse código em arquivos do GitHub.

Após a criação inicial, o bootstrap passa a recusar novas criações de administrador.

## Cadastro público

Depois de entrar como admin:

1. Abra **Administração**.
2. Entre no **Comando 06 — Cadastro público**.
3. Ative a chave.

A alteração é salva no Supabase e passa a valer para todos os dispositivos. Não é mais necessário editar `site-config.js`.

## Persistência

- Login e senha: Supabase Auth.
- Perfis: tabela `profiles`.
- Dados financeiros: `user_state`.
- Configuração global: `app_settings`.
- Mensagens: `messages` e `message_reads`.
- Auditoria: `audit_logs`.
- Acesso por usuário é protegido por Row Level Security (RLS).

## Segurança

O HTML contém apenas a publishable key do Supabase, apropriada para aplicações web públicas com RLS. Chaves administrativas permanecem somente nas Edge Functions do Supabase.


## Correção v9.1
- Corrige a detecção do bootstrap inicial do administrador no Supabase Edge Functions.
- Envia a publishable key no cabeçalho `apikey` nas chamadas de bootstrap.
