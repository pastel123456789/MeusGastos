1 GastosViewModel() em vez de viewModel(): cada recomposição cria um ViewModel novo, então o estado se perde. Ao digitar uma letra, a lista de gastos some.

2 mutableListOf em vez de mutableStateListOf: o Compose não observa mudanças nessa lista, então a tela não é avisada. Ao adicionar, a lista pode aparecer porque descricao é limpa e isso dispara recomposição. Ao remover, nada na tela muda.

3 Total em variável: com 3 gastos e 1 removido, o total mostra o valor dos 3, porque o remover() não o atualiza.

4 ViewModel com GastoRepositoryMemoria() fixo: a troca da Etapa 6 deixa de ser “uma palavra”. O tipo da propriedade é a classe concreta, então é preciso mexer no ViewModel, e você perde a injeção por construtor (não dá para passar uma implementação falsa em testes). Se atribuir o Demo, o compilador reclama de tipo incompatível.

5 if (vm.descricao.isNotBlank()) no onClick: funciona em uma tela, mas a regra fica presa na UI. Uma segunda tela de cadastro teria que duplicar o if, e as duas podem divergir. Também não dá para testar a regra sem emulador, e as outras validações (valor numérico e positivo, erro) se perdem. O lugar certo é o ViewModel.
