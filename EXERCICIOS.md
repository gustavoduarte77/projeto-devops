# Exercícios de DevOps com GitHub Actions

## Parte 1 — Workflow e checkout

Em **Actions**, abra **Deploy do Laboratório DevOps**. O job final tem o identificador `publicar-site` e aparece como **Publicar site**. Use **Run workflow** com `sem-checkout` para pular o checkout da validação. O smoke test falha porque o runner ainda não tem o arquivo do repositório. Rode `sucesso` para conferir a recuperação e registrar o nome do workflow e do job.

## Parte 2 — Dependências, smoke test e artefato

| Cenário | Resultado esperado |
| --- | --- |
| `falha-validacao` | O passo termina com código 1 e a publicação é pulada por causa de `needs`. |
| `sem-index` | O runner renomeia o arquivo antes do smoke test, que termina com código 1. |
| `caminho-inexistente` | A etapa de empacotamento falha ao tentar acessar a pasta inexistente. |
| `sucesso` | A validação passa, o artefato `github-pages` é enviado e o job final o publica. |

Na execução bem-sucedida, salve o log completo de **Validação do site**, incluindo **Smoke test do index.html**. Na mesma execução, registre a seção **Artifacts** e o resultado de **Publicar site**.

## Parte 3 — Runner

O roteiro usa `ubuntu-latest`. Em 23/11/2026, as notas oficiais anunciam a migração de Ubuntu 24.04 LTS para 26.04 LTS em novembro. Use o próprio log de **Explorando o Runner** como evidência da versão efetivamente usada. Registre distribuidor, release e codinome de `lsb_release -a`, a memória em `free -h` e o número de CPUs em `nproc`. [Notas oficiais das imagens](https://github.com/actions/runner-images/releases)

| Aspecto | Vantagem do self-hosted | Desvantagem do self-hosted |
| --- | --- | --- |
| Custo | Pode aproveitar infraestrutura ociosa e ser econômico com uso constante. | A equipe paga pela capacidade, pela energia ou pelas VMs e pelo tempo de operação. |
| Controle | Permite escolher hardware e ferramentas e acessar serviços da rede privada. | A equipe assume a configuração do isolamento, da rede e do controle de acesso. |
| Manutenção | Permite programar atualizações e manter dependências previamente instaladas. | A equipe é responsável por aplicar patches, monitorar o runner e recuperar falhas. |

## Parte 4 — Isolamento e depuração

Execute `isolamento`. O job independente instala e executa `cowsay`. Mesmo depois que esse job termina, o teste no job de publicação deve falhar porque ele recebe uma VM diferente.

Faça uma alteração visível no título ou na cor de `index.html`, faça o commit e envie para `main`. Na execução, acompanhe a preparação do runner, o checkout, o smoke test, o empacotamento, o deploy e os passos de pós-execução.

Execute `comando-inexistente` e abra **Executar comando inexistente**. O shell tenta executar a linha `comando_que_nao_existe`. Como o executável não existe no ambiente, a saída esperada é `command not found` e o código de saída é 127. A correção é remover essa chamada ou substituí-la por um comando disponível. Rode `sucesso` para confirmar a recuperação. Capture a mensagem e a linha mostradas no log real, além da execução corrigida.

## Executar no GitHub

Envie este projeto para um repositório próprio com a branch `main` e escolha **Settings → Pages → Build and deployment → Source → GitHub Actions**. As opções manuais reproduzem as falhas no runner. Para seguir literalmente os commits intermediários do enunciado, aplique as mesmas mudanças temporárias no YAML ou no HTML e reverta-as entre os testes.

Os logs, as medições e as capturas devem ser coletados das execuções reais desse repositório.
