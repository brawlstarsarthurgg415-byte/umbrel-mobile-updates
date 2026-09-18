# umbrel-mobile-updates

Repositório de atualizações do **Umbrel OS Mobile** — o painel de servidor doméstico que roda direto no celular Android, via Termux + proot-distro (Ubuntu).

Esse repo não é o código do painel em si. Ele só guarda os **pacotes de atualização** (`.zip`) que o painel baixa e aplica sozinho pela aba **Updates**.

## Estrutura

```
releases/        pacotes de atualização (.zip), um por versão
latest.json       aponta sempre para a versão mais recente
README.md         este arquivo
```

Cada `.zip` dentro de `releases/` segue o formato que o painel espera:

```
manifest.json       { "version": "x.y.z", "description": "..." }
post_install.sh      (opcional) roda automaticamente depois de aplicar
files/                arquivos que substituem os do painel (app.py, etc.)
```

## `latest.json`

É o arquivo que o painel consulta pra saber se existe uma versão nova. Formato:

```json
{
  "version": "2.7.0",
  "description": "Resumo curto do que mudou nessa versão",
  "download_url": "https://github.com/SEU-USUARIO/umbrel-mobile-updates/releases/download/v2.7.0/apps_update_2_7_0.zip"
}
```

- **version** — comparada com a versão instalada; só avisa quando for maior.
- **download_url** — link direto pro `.zip` dessa versão (pode ser um link de Release do GitHub ou o `raw.githubusercontent.com` do arquivo em `releases/`).

## Como conectar o painel a este repositório

1. Pegue o link **raw** do `latest.json`:
   `https://raw.githubusercontent.com/SEU-USUARIO/umbrel-mobile-updates/main/latest.json`
2. No painel, vá em **Updates** → cole esse link no campo de URL do manifesto remoto → salvar.
3. O painel passa a checar essa URL sozinho e avisa quando `latest.json` apontar uma versão mais nova que a instalada.

## Como publicar uma versão nova

1. Suba o novo `.zip` em `releases/` (ou crie uma Release do GitHub com o arquivo anexado).
2. Atualize o `version`, `description` e `download_url` do `latest.json` apontando pro novo arquivo.
3. Pronto — na próxima checagem, o painel já oferece a atualização.

## Histórico

| Versão | Resumo |
|---|---|
| 2.4.0 | Redesign visual da tela inicial e login (só CSS) |
| 2.7.0 | "apps update" — corrige instalação via APT, adiciona Firefox (repositório oficial da Mozilla), Jellyfin, Pi-hole e Desktop remoto |
