# Nikkei — site (front-end)

React + Vite. Conectado a dois back-ends:

| Serviço | Pasta | Porta | Faz o quê |
|---|---|---|---|
| contMB | `contMB` | 3002 | contas, login (JWT), carrinho da conta, login com Google |
| prodMB | `prodMB` | 3001 | produtos e pedidos (baixa o estoque na compra) |

## Rodar localmente
1. Suba os dois back-ends (`npm install` e `npm run dev` em cada pasta, com o `.env` de cada um; os dois usam o **mesmo `JWT_SECRET`**).
2. Neste projeto: copie `.env.example` para `.env`, ajuste se precisar, depois `npm install` e `npm run dev`.

## Produção (Vercel)
No projeto do **site**: Settings → Environment Variables → `VITE_API_URL` (URL do contMB) e `VITE_PRODUTOS_API_URL` (URL do prodMB), sem barra no final → novo deploy. Sem isso o site tenta falar com `localhost` e não carrega os produtos.

## O que cada tela usa
- **Produtos / página do produto:** `GET /api/produtos` (público).
- **Cadastrar, editar e excluir produto:** só administrador (o servidor confere o token).
- **Login / cadastro / Google:** contMB. O administrador entra pela aba "Administrador" com a conta definida no `.env` do contMB (`ADMIN_EMAIL` / `ADMIN_PASSWORD`).
- **Carrinho:** fica no navegador e, logado, sincroniza com a conta (contMB).
- **Finalizar compra / Minhas compras / Compras no painel:** prodMB.
