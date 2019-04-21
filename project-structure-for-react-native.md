# Minha estrutura de projeto para React Native

  Há tempos adio minha estreira em artigos técnicos por diversos motivos que eu nem consigueria explicar aqui. E, de fato, se eu começasse a explicar isso se tornaria um artigo sobre saúde mental e sindrome do impostor (olha o motivo ai), mas, como eu disse no inicio, este é um artigo técnico sobre o que está escrito no título.

  Este artigo está sendo impulsionado pelo novo album do **Periphery** (Periphery IV: HAIL STAN). Talvez melhor album de Djent/Metal Core dos últimos tempos? Pesado, melódico, tocante, ótimo pra desestressar. 

  Antes de começar eu queria estabelecer algumas verdades para que você tenha em mente ao ouvir a minha explicação e o por quê de eu (e o pessoal do meu time) utilizar estrutura de projeto. Ela foi criada no meu segundo ano como desenvolvedor React Native com algumas coisas em mente:

  1) Nossa estrutura anterior gerava mais bagunça do que suporte para o time
  2) Estávamos iniciando a adição de Redux para alguns projetos um pouco mais complexos

  Eu acredito que o maior problema até então, e talvez seja por isso que você tenha chegado a esse artigo, **é que não ter uma estrutura de pastas clara de leva a falta de padrão**, a famosa bagunça, arquivos gigantes e ninguém consegue dar manutenção nem nas próprias coisas (bugs). E sofrendo por esses problemas durante toda a minha vida como dev eu me tornei fascinado em estruturas e como melhora-las em prol do time.
  
  Porém esta não é uma estrutura absoluta! Meu principal objetivo com esse artigo é compartilhar essa idea e ouvir a opinião de vocês. Eu quero saber o que vocês mudariam ou se isso ajudou vocês a resolver algum problema.
  
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

### Gemfile e Fastlane

Provavelmente eu vou escrever um artigo explicando qual o meu fluxo com o [fastlane](https://fastlane.tools/). Mas vamos iniciar com o que é o fastlane:

> The easiest way to build and release mobile apps. fastlane handles tedious tasks so you don’t have to.

Simples assim. Gosto de pensar nele como um [gulp.js](https://gulpjs.com/) feito para desenvolvimento do aplicativos nativos. A pasta fastlane contém todas as configurações e informações necessárias relacionadas as plataformas iOS/Android. O Gemfile é o equivalente ao package.json para Ruby, que é a linguagem na qual o fastlane foi construído, portanto serve para que todo o time esteja alinhado em dependências relacionadas ao fastlane e para que todos tenhamos o próprio fastlane instalado.

Prometo editar esse post e adicionar o link (quando estiver disponível) do meu fluxo com o fastlane.

### babel.config.js

Tá. Isso não é anormal, mas eu gostaria de mostrar o interior dele para vocês:

```javascript
module.exports = {
  presets: ['module:metro-react-native-babel-preset'],
  plugins: [
    ['module-resolver', { root: ['./app'] }]
  ]
}
```

Module resolver? Sim, eu já sofri muito tendo que escrever require/import com caminhos muito longos e essa é a forma que eu encontrei (tanto com essa estruta ou não) de ser o mais objetivo possível ao escrever os caminhos podendo iniciar qualquer um deles iniciando com alguma pasta dentro de app que seriam os módulos do app. Ex.:

**Considerando a estrutura abaixo:**
```
app
├── Master.js
└── utils
    ├── to-money.js
    └── pluck-uniq.js
```

**Independente de onde estivermos dentro do código, podemos escrever sem medo:**
```javascript
import toMoney from 'utils/to-money';
import pluckUniq from 'utils/pluck-uniq';
```

Clean and beaultiful. Lembrando que isso funciona em qualquer parte do código por causa do babelzinho e esse plugin que nos ajuda demais da conta (sô).

Pra frizar esse exemplo, quero dar um exemplo do que poderia ser caso não utilzassemos o Module Resolver:

```javascript
import toMoney from '../../../../../../../utils/to-money';
import pluckUniq from '../../../../../../../utils/pluck-uniq';
```

> Exagero? Sim, mas passou de um `../` eu já quero morrer.

Mas Bruno, não poderiamos usar um package.json dentro de app com o name igual a app e importarmos tudo com app antes conforme o exemplo abaixo?

```javascript
import toMoney from 'app/utils/to-money';
import pluckUniq from 'app/utils/pluck-uniq';
```

Sim. Mas eu não quero.

