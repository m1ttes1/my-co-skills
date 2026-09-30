# Prompt de instalação

Cole o bloco abaixo no Claude Code do PC onde quer instalar. Não precisa de admin nem de script: o Claude faz a cópia, o backup e a mesclagem.

````
Instale a configuração do repositório my-co-skills neste computador. Trabalhe em etapas e me mostre o resultado de cada uma.

ETAPA 1: obter os arquivos
- Clone https://github.com/m1ttes1/my-co-skills.git em uma pasta temporária do meu perfil (por exemplo %TEMP%\my-co-skills).
- Se o clone falhar por autenticação, pare e me mostre o erro. Não peça nem use token. Nesse caso eu te passo os arquivos por outro meio.

ETAPA 2: conferir antes de copiar (não altere nada ainda)
- Liste o que existe hoje em ~/.claude (CLAUDE.md, agents, skills, commands, gosto-visual.md).
- Liste o que o repo traz e aponte qualquer arquivo que sobrescreveria algo existente.
- Espere meu OK.

ETAPA 3: instalar (depois do meu OK)
1. Backup: copie o que for ser tocado para ~/.claude/backups/my-co-skills-AAAA-MM-DD/.
2. Copie agents/*, skills/* e commands/* do repo para as pastas equivalentes em ~/.claude, sem apagar nada que já exista e não seja do repo.
3. CLAUDE.md: NÃO sobrescreva o meu. Insira o conteúdo de global/CLAUDE.md dentro de um bloco delimitado por <!-- my-co-skills:start --> e <!-- my-co-skills:end -->. Se o bloco já existir, substitua só o que estiver entre os marcadores. Se ~/.claude/CLAUDE.md não existir, crie com o bloco. Não altere nada fora do bloco.
4. gosto-visual.md: copie para ~/.claude/gosto-visual.md somente se não existir ou estiver vazio. Se já tiver conteúdo, não toque.
5. Não mexa em settings.json, credenciais, plugins nem em nenhuma outra pasta.

ETAPA 4: verificar
- Confirme que cada SKILL.md e cada arquivo de agents/ começa com frontmatter YAML válido.
- Mostre a árvore final do que foi instalado e o que foi para o backup.
- Apague a pasta temporária do clone.
- Me diga para reiniciar o Claude Code (ou abrir uma sessão nova) para as skills carregarem.

Regras: não faça commit nem push de nada, não crie repositórios, não altere configuração global do git, não use admin.
````

## Atualizar depois

Cole o mesmo prompt de novo. O bloco do CLAUDE.md é substituído pelo marcador, o backup guarda a versão anterior e o `gosto-visual.md` com conteúdo nunca é sobrescrito.
