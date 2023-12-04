
# GIT-101

Merhaba, bu yazımda daha önce hiç git kullanmamış birine, en basit haliyle git anlatmaya çalışacağım. Git bir versiyon kontrol sistemidir. Kısaca uygulamamız üzerinde geliştirme , düzeltme vb. işlemler yaptığımızda git kullanarak uygulamalarınızın en güncel halini yayınlayabiliriz ya da dosyalarımızı remote'a aktararak bir depo olarak da kullanabiliriz 
Öncelikle bir dosya ya da dizin yapısında git'i başlatmak için aşağıdaki komutu kullanırız.
> ---$ git init

Git'te kullanıcı kimlik bilgilerini belirlemek için ise aşağıdaki komutlar kullanılır. Bu komutlar, yaptığınız commitlerde görünen kullanıcı adını ve mailini belirler.

>---$ git config --global user.name "Fatih"
---$ git config --global user.email "fatih@aydin.com"

## Staging

 Git'te "staging" kavramı, değişikliklerin bir sonraki commit'e eklenmeden önce geçici bir alanda bekletilmesini ifade eder. Bu aşama, değişikliklerin commit işlemine eklenmeden önce dikkatlice kontrol edilmesine ve gerektiğinde düzenlemelere olanak tanır.

### Stage your changes:

>Add to index / stage
---$ git add file.txt
 Add all modified and new files (tracked or not) to index
---$ git add -A
Partial staging
---$ git add -p file.txt

  

## Commit
  
Git'te "commit," projenizdeki değişikliklerin kalıcı olarak kaydedildiği bir işlemi ifade eder. Her commit, projenizdeki belirli bir anın bir görüntüsünü temsil eder ve projenizin geçmişinde izlenebilir. Commit işlemleri, projenizde yapılan her türlü değişikliği içerebilir, yeni dosya eklemek, mevcut dosyaları düzenlemek veya dosyaları silmek gibi.
> Commit from index
---$ git commit
Commit from tracked file list
---$ git commit file1.txt file2.txt
All modified tracked files
---$ git commit -a
Commit from pattern
---$ git commit **/*.py

Aşağıdaki git status komutu, çalışma dizininizde ve depoda (repository) hangi dosyaların değiştiğini, hangi dosyaların staged (hazır durumda) olduğunu ve hangi dosyaların commit beklediğini kontrol etmek için kullanılır.
>---$ git status
> Tüm commit geçmişini görüntüler.
---$ git log
Son 5 commit'i getirir.
 ---$ git log -5
İki branch arasındaki farkları görüntülemeni sağlar.
 ---$ git log origin/master..master
## Stash
Stash, bir nevi "raf" olarak düşünülebilir. Eğer üzerinde çalıştığınız bir konuda değişiklikler yaptınız ancak bunları commit etmek istemiyorsanız veya başka bir branch'e geçmek istiyorsanız, `git stash` kullanabilirsiniz. Bir nevi yaptığınız değişiklikleri rafa kaldırıyorsunuz.
> Create a stash
---$ git stash
list stashes
---$ git stash list
 Apply a stash
---$ git stash apply
Apply a stash and drop it
---$ git stash pop
Clear your stashes
---$ git stash clear
## Undoing
Git'te yapılan değişiklikleri geri almak veya bir önceki duruma dönmek  için kullanılır.
>  Yeni bir commit oluşturur ve seçilen commit'teki değişiklikleri geri alır.
---$ git revert 
En son commit'inizi değiştirmenizi sağlar.
---$ git commit --amend
Belirli bir dosyanın staging alanındaki değişikliklerini geri alır.
---$ git reset --mixed HEAD file
Belirli bir dosyadaki değişiklikleri geri alır ve dosyayı en son commit haline getirir.
---$ git checkout file
Belirli bir commit veya referans noktasına (branch veya tag) kadar olan tüm değişiklikleri siler.
---$ git reset --hard ref
## Branching and merging
Yazılım geliştirme süreçlerinde paralel geliştirme yapma, yeni özellikler ekleyerek veya hataları düzelterek kod tabanını güncelleme ve farklı geliştiricilerin aynı anda aynı projada çalışmasını kolaylaştırır.
> ---$ git branch feature # Create the branch
---$ git checkout feature # Switch to the new branch
---$ git checkout -b feature # or in a single command

![https://illustrated-git.readthedocs.io/en/latest/_images/git-branch-create.svg](https://illustrated-git.readthedocs.io/en/latest/_images/git-branch-create.svg)

## Branche diverging
Başlangıçta aynı commit'te olan iki branch, daha sonra developerlar tarafından yapılan değişiklikler nedeniyle farklı commit'leri işaretler. Bu durum, branch'in birleştirilmeden önce farklı hale geldiği anlamına gelir. Örneğin, "master" ve "feature" adlı iki branch düşünelim. İki branch'te başlangıçta aynı commit'te olabilir, ancak geliştiriciler farklı özellikler eklerken veya hataları düzeltirken, branchler birbirinden farklı commit'leri işaretler. Bu durumda, bu iki branch "diverging" durumundadır. Bu durum sonrasında conflict oluşturabilir 

![enter image description here](https://illustrated-git.readthedocs.io/en/latest/_images/git-branch-diverge.svg)

## Merge
Genellikle, iki ayrı branch'in geliştirildiği durumlar söz konusu olduğunda, bu değişiklikleri tek bir branch'de  birleştirmek amacıyla merge işlemi kullanılır.
>master branch'ine geçiş yap 
--- $git checkout master
 feature-branch'ini master ile birleştir 
 --- $git merge feature-branch

![enter image description here](https://illustrated-git.readthedocs.io/en/latest/_images/git-branch-merge.svg)
  

## Rebase
Rebase işlemi sırasında, seçilen branch'teki commit'ler, hedef branch'in en son commit'ine uygulanır. Bu, commit geçmişini daha temiz, düzenli ve doğrusal bir hale getirmeyi amaçlar.

> ---$ git rebase master
 or interactive version
---$ git rebase -i master

![enter image description here](https://illustrated-git.readthedocs.io/en/latest/_images/git-branch-rebase.svg)

## Cherry Pick
Commit geçmişinizden belirli değişiklikleri alıp, bunları başka bir branch'te kullanmanıza olanak tanır. Bu işlem, belirli değişiklikleri veya özellikleri seçip almak istediğinizde kullanışlıdır.

> ---$ git cherry-pick

![enter image description here](https://illustrated-git.readthedocs.io/en/latest/_images/git-cherry-pick.svg)

##  Working with remote repositories
Remote repo ile çalışmak, Git'in işbirliği ve paylaşım yeteneklerinden yararlanma sürecidir. Projelerinizi başka developerlarla paylaşmak, değişiklikleri takip etmek ve güncellemek istediğinizde, remote repository'ler kullanılır.

> Remote ekleme
>---$ git remote add origin fatihtrysomething
Eklediğiniz remote repoları görüntüleme
---$ git remote -v
Remote repositoryden projenize yeni değişiklikleri çekmek
---$ git fetch origin
Remote repodaki değişiklikleri birleştirme
---$ git merge origin/master
Remote'a göndermek için
---$ git push origin master

![enter image description here](https://illustrated-git.readthedocs.io/en/latest/_images/git-flows.svg)

