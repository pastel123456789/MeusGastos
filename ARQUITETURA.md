1. Se o app passar a buscar os gastos de uma API, quais arquivos mudam e quais não?

Mudam: só o model/GastoRepository.kt. Também muda a linha do ViewModel onde a implementação padrão é escolhida Não mudam: Gasto.kt, Categoria.kt, a interface GastoRepository, as regras do ViewModel e todos os arquivos de ui/.o ViewModel depende da interface, não da implementação. Quem consome só conhece listar, adicionar e remover.

2. Por que o total é calculado e não guardado? Qual bug apareceria?

Se o total fosse uma variável atualizada à mão, cada função que mexe na lista  precisaria lembrar de atualizá-lo.
Bug concreto: adicionar 3 gastos, remover 1, e o total continua somando os 3. Outro caso é o filtro, que mudaria a lista visível sem mudar o total.
Calculado a partir de gastosVisiveis, ele não tem como ficar dessincronizado e já respeita o filtro.

3. O que o FormularioGasto não receber o ViewModel permitiu fazer?

Criar @Preview do componente em qualquer situação, inclusive a tela de erro, passando erro = "..." direto, sem rodar o app nem provocar o erro.
Reaproveitar o componente em outra tela.
Não depender de um ViewModel real nem de repositório para desenhar nada.
