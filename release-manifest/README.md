# PitChase launcher manifest no GitHub

O `PitChaseLauncher.exe` agora pode trabalhar com um manifesto estatico no GitHub, sem depender da leitura da pasta de patch em um servidor local.

## Fluxo

1. Suba os arquivos do patch como assets de um release no repositório `JpAndreBTA/PitC-Game`.
2. Edite `release-manifest/manifest.json`.
3. Para cada arquivo publicado, preencha:
   - `relative_path`: caminho final dentro da pasta do jogo
   - `size`: tamanho em bytes
   - `sha256`: hash SHA-256 do arquivo publicado
   - `updated_at`: data ISO UTC
   - `download_url`: link direto do asset no release
4. Atualize `version`, `manifest_token`, `file_count`, `total_size` e `generated_at`.
5. Faça commit do `manifest.json`.

## Resultado esperado

- O launcher baixa apenas arquivos faltando ou diferentes.
- Se o `manifest.json` mudar, mas os arquivos locais ja estiverem corretos, ele apenas grava o novo token e nao baixa nada.
- A leitura inicial vira uma unica requisicao do manifesto, em vez de ficar dependendo de busca local no host.
