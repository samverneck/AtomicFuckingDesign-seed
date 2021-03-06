# Atomic FUCKING Design seed

> Antes de tudo, indico esse livro para que vocë possa entender essa nomenclatura.

![uma breve história do tempo](https://i1.zst.com.br/images/uma-breve-historia-do-tempo-capa-comum-9788580576467-photo44272988-12-29-d.jpg)

> Brinks! Mas indico o livro fortemente porque ele é do **CARALHO**!

Arquitetura modular e atômica criada no [Be MEAN]() para facilitar a vida dos programadores **vagabundos** como eu.

> Por que ficar copiando e colando código toda vez que irá iniciar um projeto?

Pensando na minha preguiça de velho modularizei **tudo** que podia para facilitar minha vida e a de vocês.

> Quanto mais você fizer, menos terá que fazer no futuro.

> **Como isso tio Suissa?**

Pense comigo: quantas vezes na sua vida você usou o campo `name`?

Cheguei num limite de não aceitar refazer mais nenhum código e percebi diversos padrōes neles, fui refatorando para deixa-los o mais genérico possível e de uma forma onde tudo que é criado será um módulo que poderá ser reutilizado em **qualquer outra parte do sistema.**

Por exemplo:

> O campo `name` é um módulo atômico que pode ser reutilizado em qualquer outro módulo que o necessite, como também em qualquer outro sistema que você fizer.

> Ou seja, quanto mais sistemas você fizer menos terá que fazer.


## Idéia 

Essa arquitetura atômica foi baseada na minha arquitetura de Atomic Design Behavior do frontend, porém nessa eu fui longeeeeee.

Basicamente você **NUNCA** irá iniciar **NADA** com um arquivo novo, **SEMPRE** irá abrir um já existente e deve salva-lo com outro nome e aí sim colocar sua lógica.

Existem apenas 3 pastas onde você poderá criar arquivos novos:

- _atoms
- _organelles
- _quarks

**NUNCA mexa nos arquivos dentro de:**

- _factories
- _hadrons

Sobrando a pasta de `modules` a qual armazena os módulos que usarão os módulos atômicos


Caso você ainda não esteja habituado com esses termos de Física Quântica (quarks, hadrons), Química


## Arquitetura

Para facilitar a visualização dessa arquitetura montei esse simples Diagrama de Venn, onde podemos ver que o *Organism* é composto de:

- *Molecule*
- *Organelle*

A *Organelle* é a função que será executada quando houver uma requisição em uma rota, sua resposta será devolvida pelo *Ribosome*.

A *Molecule* é a definição da estrutura dos campos (*Atoms*) os quais são validados pelos *Quarks*.


![](http://i.imgur.com/zZQpbBN.png)

> **Por acaso você é louco???**


> Sim, mas isso não vem ao caso. Posso explicar-lhe o porquê dessa nomenclatura, acompanhe-me na minha viagem.

**Tudo começou com o átomo...**

Inicialmente questionei-me: 

> Sempre uso o campo `name` em vários *Schemas/Molecules* **por que não modularizar essa PORRA???**

Vamos analisar como é o campo `name` no *Schema* do Mongoose:

```js
const schema = {
  name: {
    type: String,
    required: [true, 'name is required']
    validate: {
      validator: (v) => /[a-zA-Z]/.test(v)
      },
      message: '{VALUE} its not only letters!'
    }
  }
}
```

Na minha lógica separei em duas partes:

```js
const ATOM_NAME = 'name'

const PROPS = { 
  type: String
  required: [true, 'name is required']
}

const VALIDATE = {
  validate: {
    validator: (v) => /[a-zA-Z]/.test(v)
    },
    message: '{VALUE} its not only letters!'
  },
}

const schema = {
  [ATOM_NAME]: {
    PROPS,
    VALIDATE
  }
}
```

Eu nomeei de Átomo a configuração de `PROPS` e de Hádron o objeto de `VALIDATE`.

> **Suissa por que raios você chamou de Hádron?**


> Hádron, em Física de Partículas, é uma partícula composta, formada por um estado ligado de quarks.

*fonte: https://pt.wikipedia.org/wiki/H%C3%A1dron*


Então vamos analisar nosso objeto:

```js
const VALIDATE = {
  validate: {
    validator: (v) => /[a-zA-Z]/.test(v)
    },
    message: '{VALUE} its not only letters!'
  },
}
```

Mesmo o Hádron sendo formado por 3 Quarks, nesse caso teremos apenas 2:

- validator
- message

