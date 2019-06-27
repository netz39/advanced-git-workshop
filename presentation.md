---
title: Netz39 -- Advanced Git Workshop
tags: Git, Workshop, Workshop, 
description: Slides für den Git Workshop im Netz39
---

# Git Workshop

## von therojam & zip

---

Wir werde das interaktiv machen
bitte holt eure Laptops raus!

---

## Was ist denn GIT noch mal?

[![](https://imgs.xkcd.com/comics/git.png)](https://xkcd.com/1597/)


---

## Git Commit

[![](https://imgs.xkcd.com/comics/git_commit.png)](https://xkcd.com/1296/)

---

## TOP

- git branches
- git forks
- git submodule
- git lfs und git annex
---

## Arbeit mit Branches und Forks

- Einsatz für Arbeit in Eigenregie
- Kollaboration
---

### Einsatz für Arbeit in Eigenregie

- Arbeit an Features (feature workflow)
- Nutzung als Ablage (stash)
- git reset/rebase[--interactive]/log [--reflog,--pretty-format,...]
- git commit --amend
---

### Kollaboration

- Feature Branches (git-flow workflow)
- Forks / Pull/Merge Requests (fork workflow)
- git pull --rebase
---

## git submodule

- Einsatzgründe, sowie Vor- und Nachteile
- - Submodule können erstellt und modifiziert werden
- - Verwendung von git submodule foreach [--recursive]
- - Einsatz von Tracking Branches in Submodulen
- - Rekursives Handling von Checkout, Clone, Push/Pull
---

## git lfs


{%youtube 9gaTargV5BY %}
 
 --- 

 ## git annex



 ---

 ## Offene Fragen?

 ---

 ### Usage flow

 ---


 ```graphviz
 digraph {
   compound=true
     rankdir=RL

       graph [ fontname="Source Sans Pro", fontsize=20 ];
         node [ fontname="Source Sans Pro", fontsize=18];
           edge [ fontname="Source Sans Pro", fontsize=12 ];


             subgraph core {
                 c [label="Hackmd-it \ncore"] [shape=box]
                   }
                     
                       c -> sync [ltail=session lhead=session]

                         subgraph cluster1 {
                              concentrate=true
                                  a [label="Text source\nGithub, Gitlab, ..."] [shape=box]
                                      b [label="HackMD Editor"] [shape=box]
                                          sync [label="sync" shape=plaintext ]
                                              b -> sync  [dir="both"]
                                                  sync -> a [dir="both"]
                                                      label="An edit session"
                                                        }
                                                        }
                                                        ```

                                                           ---

                                                           ### Architecture of extension

                                                           ---

                                                           ![](https://i.imgur.com/ij69tPh.png)

                                                           ---

                                                           ## Content script

                                                           - Bind with each page
                                                           - - Manipulate DOM
                                                           - - Add event listeners
                                                           - - Isolated JavaScript environment
                                                           -   - It doesn't break things
---

# :fork_and_knife: 

---

<style>
code.blue {
  color: #337AB7 !important;
  }
  code.orange {
    color: #F7A004 !important;
    }
    </style>

    - <code class="orange">onMessage('event')</code>: Register event listener
    - - <code class="blue">sendMessage('event')</code>: Trigger event
---

# :bulb: 

---

- Dead simple API
- - Only cares about application logic
---

```typescript
import * as Channeru from 'channeru'

// setup channel in different page environment, once
const channel = Channeru.create()
```

   ---

   ```typescript
   // in background script
   const fakeLogin = async () => true

   channel.answer('isLogin', async () => {
     return await fakeLogin()
     })
     ```

        <br>y<y<y

        ```typescript
        // in inject script
        const isLogin = await channel.callBackground('isLogin')
        console.log(isLogin) //-> true
        ```

           ---

           # :100: :muscle: :tada:

           ---

           ### Wrap up

           - Cross envornment commnication
           - - A small library to solve messaging pain
           - - TypeScript Rocks :tada: 
---

### Thank you! :sheep: 

You can find me on

- or email me
-
