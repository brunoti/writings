# Minha estrutura de projeto para React Native

  Há tempos adio minha estreira em artigos técnicos por diversos motivos que eu nem consigueria explicar aqui. E, de fato, se eu começasse a explicar isso se tornaria um artigo sobre saúde mental e sindrome do impostor (olha o motivo ai), mas, como eu disse no inicio, este é um artigo técnico sobre o que está escrito no título.

  Este artigo está sendo impulsionado pelo novo album do Periphery (Periphery IV: HAIL STAN). Talvez melhor album de Djent/Metal Core dos últimos tempos? Pesado, melódico, tocante, ótimo pra desestressar. 

  Antes de começar eu queria estabelecer algumas verdades para que você tenha em mente ao ouvir a minha explicação e o por quê de eu (e o pessoal do meu time) utilizar estrutura de projeto. Ela foi criada no meu segundo ano como desenvolvedor React Native com algumas coisas em mente:
  1 - Nossa estrutura anterior gerava mais bagunça do que suporte para o time
  2 - Estávamos iniciando a adição de Redux para alguns projetos um pouco mais complexos
  Eu acredito que o maior problema até então, e talvez seja por isso que você tenha chegado a esse artigo, **é que não ter uma estrutura de pastas clara de leva a falta de padrão**, a famosa bagunça, arquivos gigantes e ninguém consegue dar manutenção nem nas próprias coisas (bugs). E sofrendo por esses problemas durante toda a minha vida como dev eu me tornei fascinado em estruturas e como melhora-las em prol do time. Porém esta não é uma estrutura absoluta! Meu principal objetivo com esse artigo é compartilhar essa idea e ouvir a opinião de vocês. Eu quero saber o que vocês mudariam ou se isso ajudou vocês a resolver algum problema.
  Como exemplo eu vou utilizar um projeto pessoal meu o **Copia Libri**, que é um aplicativo para gerencias vendas de livros que ocorrem na livraria da igreja em que faço parte (8ª Igreja Presbiteriana de Franca). Não vou mostrar muito do código por motivos de está zuado e não é o objetivo também. No desenrolar da estrutura vocês vão ver algumas libs e talvez coisas meio estranhas que não necessáriamente tem a ver com estrutura de pastas, talvez depois eu faça um artigo sobre cada uma dessa coisas (me cobrem). 

## Primeiro Nível (tree -L 1)
```
.
├── android
├── app
├── app.json
├── babel.config.js
├── fastlane
├── scripts
├── index.js
├── ios
├── node_modules
├── package.json
├── Gemfile.lock 
├── Gemfile
└── yarn.lock
```

Como vocês já conhecem a maioria dos itens contidos nessa base eu vou comentar somente sobre as anormalidades.

### babel.config.js
