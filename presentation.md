---
title: Netz39 -- Advanced Git Workshop
tags: Git, Workshop, Workshop, 
description: Slides für den Git Workshop im Netz39

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

# Advanced Git Workshop

## von therojam & zipzob

<!-- [TOC] -->

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

## Was ist denn GIT noch mal?  :information_source:

[![](https://imgs.xkcd.com/comics/git.png)](https://xkcd.com/1597/)


---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

## Git Commit  :arrow_right_hook:

[![](https://imgs.xkcd.com/comics/git_commit.png)](https://xkcd.com/1296/)

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

## running order :memo: 

- git branches 
- git forks
- git submodule
- git lfs

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Arbeit mit Branches und Forks  :twisted_rightwards_arrows:

- branch
   - github.com/netz39
- Fork

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Einsatz für Arbeit in Eigenregie  :bust_in_silhouette:

- Arbeit an Features/Update (feature workflow)
- Nutzung als Ablage (stash)
- git reset/rebase [--interactive]/log [--reflog,--pretty-format,...]
- git commit --amend, git push --force

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->


### Teamwork :dancers: 

[![](https://static.bocoup.com/blog/git-workflow/git_diagrams.png)](https://bocoup.com/blog/git-workflow-walkthrough-feature-branches)

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->


### Zusammenarbeit  :busts_in_silhouette:

- Branches 
- Forks 
- Pull/Merge Requests 
- git pull --rebase

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Arbeit mit Branches und Forks  :twisted_rightwards_arrows:

- branch
   - github.com/netz39
   - [Jasper-Ben/freifunk-praesentation](https://github.com/Jasper-Ben/freifunk-praesentation)
- Forks
    - [TheRojam/advanced-git-workshop](https://github.com/TheRojam/advanced-git-workshop)

:::info
Forks koennen auch [Mirror (Spiegel)](https://https://docs.gitlab.com/ee/workflow/repository_mirroring.html) sein.
Manchmal sind aber weitere "remotes" sinnvoller. 
z.B. Arbeit an AUR-Package
:::

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->


### Links :link: 

[Git Doc: Branching Basics](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

## git submodule  :bookmark_tabs:

<!-- - Einsatzgründe, sowie Vor- und Nachteile
- Submodule können erstellt und modifiziert werden
- Verwendung von git submodule foreach [--recursive]
- Einsatz von Tracking Branches in Submodulen
- Rekursives Handling von Checkout, Clone, Push/Pull
 -->

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Was ist es? Wozu?

- anderes (eingebundenes) Projekt, welches bereit in git versioniert ist
- Submodul Worktree liegt in Unterverzeichnis
- Versionierung des Unterverzeichnis erfolgt separat 

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

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

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Submodul anlegen/einbetten

```
$ git submodule add <repository-url> (<subfolder name>*)
```

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Aktuellen Stand der Submodule laden

```
$ git submodule update --init --recursive
```

War in älteren git-Versionen nötig, mittlerweile in <code>git submodule add</code> und <code>git clone</code>

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Clonen mit Submodulen :open_file_folder: 

```
$ git clone --recursive <project url>
```

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Git Submodule foreach

- Shellkommandos in jedem ausgechecktem Submodul ausführen
- Platzhalter für Submodulparameter

```
$ git submodule foreach 'echo $path `git rev-parse HEAD`'
```

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

- Weitere Variablen: :heavy_dollar_sign: 
    - **$name** - name of the relevant submodule section in .gitmodules
    - **$sm_path** - path of the submodule as recorded in the immediate superproject
    - **$displaypath** - relative path from the current working directory to the submodules root directory
    - **$sha1** - commit as recorded in the immediate superproject
    - **$toplevel** - absolute path to the top-level of the immediate superproject. 

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Tracking Branch :open_file_folder: 

- Bei Submodulen wird standardmäßig die Branchzugehörigkeit nicht mit betrachtet/gespeichert
- Mittels config kann das aber angepasst werden

```
$ git submodule foreach 'git config --file
  $toplevel/.gitmodules submodule.$name.branch
  `git rev-parse --abbrev-ref HEAD --`'
```

- Oder beim Intialen einrichten

```
$ git submodule add -b <branch name>
  <repository-url> <subfolder name>
```

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Rekursives Updaten

Ein Gefühl für die Variablen bekommen:
```
$ git submodule foreach --quiet --recursive
  'echo $name $displaypath $path $sm_path
  $sha1 $toplevel'
```

Submodule Bottom-Up bearbeiten:
```
$ git submodule foreach --quiet --recursive
  'echo `pwd`' | tac | xargs -I {} bash -c 'pushd "{}"
  >/dev/null; pwd ; popd >/dev/null'
```

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Pros/Cons :heavy_plus_sign: :heavy_minus_sign: 

- Git lädt die Inhalte von Submodulen nicht selbständig/automatisch nach
	- Empfehlung: Nutzt andere Varianten um Abhängigkeiten zu tracken, wenn möglich: NPM, Bower, rubygems, ...
- Da Submodule nur eine SHA-Referenz sind muss hier das Vorgehen bei Updates von Submodulen aufgepasst werden: Detached HEAD, nested push/pull, ...

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Pros/Cons :heavy_plus_sign: :heavy_minus_sign: 

- Kollegen/Zuarbeitende müssen ggf. über updates informiert werden
- Verschachtelung möglich, macht aber mit zunehmender Tiefe vieles umständlich
- Komplexe Setups werden schnell unhandlich

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Links about submodules :link: 

- [Git Docs Submodules](https://git-scm.com/docs/git-submodule)
- [Blog working-with-submodules](https://github.blog/2016-02-01-working-with-submodules/)
- [Git Book Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
- [Vogella on git submodules](https://www.vogella.com/tutorials/GitSubmodules/article.html)

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

## git worktree

- Verwalten mehrerer Working Trees aus einem Repository
- Z.B. Parallel compilen und programmieren

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

```
$ git worktree add <name-of-our-worktree> <branch-name>
```

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

```
$ git worktree list
$ git worktree prune
```

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Links :link: 

[Git Doc worktree](https://git-scm.com/docs/git-worktree)
[Git Worktrees](https://mattshomepage.com/articles/2018/Feb/16/git_worktrees/)

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

## git lfs 


{%youtube 9gaTargV5BY %}



---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### git lfs  :paperclip:

- git large file storage
- replaces large files like graphics with text pointers inside Git while storing the file contents on a remote server like GitHub
- needs packackage git-lfs (via your package manager) installed  
- 

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Links

* [git lfs](https://git-lfs.github.com/)


---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

## Further Reading :books:

* [Git Internals PDF](https://github.com/pluralsight/git-internals-pdf)
* [Pro Git book](https://git-scm.com/book/en/v2)
* [OhShitGit](http://ohshitgit.com/)
* [Atlassian - Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
* [Praqma git course summary](https://www.praqma.com/training/git-mastering)
* [subrepo](https://github.com/ingydotnet/git-subrepo)
* [Getting Started w/ git annex](https://writequit.org/articles/getting-started-with-git-annex.html)


---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### Offene Fragen?

## :question:

---

<!-- .slide: data-background="https://i.imgur.com/zfAYMlY.jpg" -->

### :100: :muscle: :tada: :heart_decoration: 
### Danke

- Jabber MUC :busts_in_silhouette: 
- Fax :fax: 
- Brief :mailbox_with_mail: 
