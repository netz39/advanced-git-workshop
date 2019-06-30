---
title: Netz39 -- Advanced Git Workshop
tags: Git, Workshop, Workshop, 
description: Slides für den Git Workshop im Netz39

---
<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

# Advanced Git Workshop

## von therojam & zipbob

<!-- [TOC] -->

---

## Was ist denn GIT noch mal?  :information_source:

[![](https://imgs.xkcd.com/comics/git.png)](https://xkcd.com/1597/)


---

## Git Commit  :arrow_right_hook:

[![](https://imgs.xkcd.com/comics/git_commit.png)](https://xkcd.com/1296/)

---

## running order :memo: 

- git branches 
- git forks
- git submodule
- git lfs

---

## Arbeit mit Branches und Forks  :twisted_rightwards_arrows:

- branch
   - github.com/netz39
   - [Jasper-Ben/freifunk-praesentation](https://github.com/Jasper-Ben/freifunk-praesentation)
- Forks
    - [TheRojam/advanced-git-workshop](https://github.com/TheRojam/advanced-git-workshop)

---

### Einsatz für Arbeit in Eigenregie  :bust_in_silhouette:

- Arbeit an Features/Update (feature workflow)
- Nutzung als Ablage (stash)
- git reset/rebase [--interactive]/log [--reflog,--pretty-format,...]
- git commit --amend, git push --force

---


### Teamwork :dancers: 

[![](https://static.bocoup.com/blog/git-workflow/git_diagrams.png)](https://bocoup.com/blog/git-workflow-walkthrough-feature-branches)

---

### Zusammenarbeit  :busts_in_silhouette:

- Branches 
- Forks 
- Pull/Merge Requests 
- git pull --rebase

---

### Links :link: 

[Git Doc: Branching Basics](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

---


## git submodule  :bookmark_tabs:

- Einsatzgründe, sowie Vor- und Nachteile
- Submodule können erstellt und modifiziert werden
- Verwendung von git submodule foreach [--recursive]
- Einsatz von Tracking Branches in Submodulen
- Rekursives Handling von Checkout, Clone, Push/Pull

---

### Was ist es? Wozu?

- anderes (eingebundenes) Projekt, welches bereit in git versioniert ist
- Submodul Worktree liegt in Unterverzeichnis
- Versionierung des Unterverzeichnis erfolgt separat 

---

```
$ git submodule foreach --help

usage: git submodule [--quiet] add [-b <branch>] [-f|--force] [--name <name>] [--reference <repository>] [--] <repository> [<path>]
   or: git submodule [--quiet] status [--cached] [--recursive] [--] [<path>...]
   or: git submodule [--quiet] init [--] [<path>...]
   or: git submodule [--quiet] deinit [-f|--force] (--all| [--] <path>...)
   or: git submodule [--quiet] update [--init] [--remote] [-N|--no-fetch] [-f|--force] [--checkout|--merge|--rebase] [--[no-]recommend-shallow] [--reference <repository>] [--recursive] [--] [<path>...]
   or: git submodule [--quiet] summary [--cached|--files] [--summary-limit <n>] [commit] [--] [<path>...]
   or: git submodule [--quiet] foreach [--recursive] <command>
   or: git submodule [--quiet] sync [--recursive] [--] [<path>...]
   or: git submodule [--quiet] absorbgitdirs [--] [<path>...]

```

---

### Submodul anlegen/einbetten

```
$ git submodule add <repository-url> (<subfolder name>*)
```

### Aktuellen Stand der Submodule laden

```
$ git submodule update --init --recursive
```
War in älteren git-Versionen nötig, mittlerweile in <code>git submodule add</code> und <code>git clone</code>

---

### Clonen mit Submodulen :open_file_folder: 

```
$ git clone --recursive <project url>
```

### Git Submodule foreach

- Shellkommandos in jedem ausgechecktem Submodul ausführen
- Platzhalter für Submodulparameter

```
$ git submodule foreach 'echo $path `git rev-parse HEAD`'
```

---

- Weitere Variablen: :heavy_dollar_sign: 
    - **$name**
        - name of the relevant submodule section in .gitmodules
    - **$sm_path**
        - path of the submodule as recorded in the immediate superproject
    - **$displaypath**
        - relative path from the current working directory to the submodules root directory
    - **$sha1**
        - commit as recorded in the immediate superproject
    - **$toplevel**
        - absolute path to the top-level of the immediate superproject. 

---

### Tracking Branch :open_file_folder: 

- Bei Submodulen wird standardmäßig die Branchzugehörigkeit nicht mit betrachtet/gespeichert
- Mittels config kann das aber angepasst werden

```
$ git submodule foreach 'git config --file $toplevel/.gitmodules submodule.$name.branch `git rev-parse --abbrev-ref HEAD --`'
```

- Oder beim Intialen einrichten

```
$ git submodule add -b <branch name> <repository-url> <subfolder name>
```

---

### Rekursives Updaten

```
$ git submodule foreach --quiet --recursive 'echo $name $displaypath $path $sm_path $sha1 $toplevel' ~

$ git submodule foreach --quiet --recursive 'echo $displaypath' | uniqu .... xargs ...

$ git submodule foreach --quiet --recursive 'echo `pwd`' | tac | xargs -I {} bash -c 'pushd "{}" >/dev/null; pwd ; popd >/dev/null'
```
----

### Pros/Cons :heavy_plus_sign: :heavy_minus_sign: 

- Git lädt die Inhalte von Submpodulen nicht selbständig/automatisch nach
	- Nutzt andere Varianten um Abhängigkeiten zu tracken, wenn möglich: NPM, Bower, rubygems, ...
- ??????? Da Submodule nur eine SHA-Referenz sind muss hier das Vorgehen bei Updates von Submodulen aufgepasst werden: Detached HEAD, nested push/pull, ...
- Kollegen/Zuarbeitende müssen ggf. über updates informiert werden
- ??? Komplexe Setups werden schnell unhandlich
- Verschachtelung möglich macht aber mit zunehmender Tiefe vieles umständlich (Wer macht sowas?)

---

### Links about submodules :link: 

- [Git Docs Submodules](https://git-scm.com/docs/git-submodule)
- [Blog working-with-submodules](https://github.blog/2016-02-01-working-with-submodules/)
- [Git Book Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
- [Vogella on git submodules](https://www.vogella.com/tutorials/GitSubmodules/article.html)
---


## git worktree ?????

- Verwalten mehrerer Working Trees aus einem Repository
- Z.B. Parallel compilen und programmieren


---

### Links :link: 

[Git Doc worktree](https://git-scm.com/docs/git-worktree)

---

## git lfs 


{%youtube 9gaTargV5BY %}


--- 


---

## git lfs  :paperclip:

- git large file storage
- [git lfs](https://git-lfs.github.com/)
- replaces large files like graphics with text pointers inside Git while storing the file contents on a remote server like GitHub
- needs packackage git-lfs (via your package manager) installed  



---

## Further Reading :books:

* [Git Internals PDF](https://github.com/pluralsight/git-internals-pdf)
* [Pro Git book](https://git-scm.com/book/en/v2)
* [OhShitGit](http://ohshitgit.com/)
* [Atlassian - Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
* [Praqma git course summary](https://www.praqma.com/training/git-mastering)
* [subrepo](https://github.com/ingydotnet/git-subrepo)
* [Getting Started w/ git annex](https://writequit.org/articles/getting-started-with-git-annex.html)

---

---

### Offene Fragen?

## :question:

---

### :100: :muscle: :tada: :heart_decoration: 
### Danke

- Jabber MUC :busts_in_silhouette: 
- Fax :fax: 
- Brief :mailbox_with_mail: 
