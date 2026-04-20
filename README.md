1. Por que a Secret aparece no log como *** e a variável aparece normalmente?
R:GitHub Actions possui um mecanismo de segurança integrado chamado Secret Masking.Quando um valor é definido como
"Secret", o runner monitora a saída padrão (logs). Se ele detectar o valor exato daquela secret sendo impresso,
ele o substitui automaticamente por asteriscos para evitar que informações sensíveis (como senhas ou tokens)
fiquem expostas no histórico do repositório. Já as "Variables" são consideradas dados de configuração não sensíveis,
por isso permanecem legíveis.

2.O Job deploy_app consegue ler a variável BUILD_VERSION criada no Job build_app? Por quê? 
R:Não. O escopo da variável BUILD_VERSION está restrito apenas ao job build_app.Cada Job no GitHub Actions roda em um Runner
(máquina virtual) diferente e isolado. Quando o build_app termina, seu ambiente é destruído. 
Para compartilhar dados entre jobs diferentes, você precisaria usar outputs ou persistir a informação em um arquivo (Artifact).
