# GitHub ile nasıl birlikte çalışılır?

Bir yazılım ekibinin git sürüm takip sistemini kullanarak ortak çalışması için
pek çok senaryo var.   Bu dokümanda örnek bir senaryo ile GitHub üzerinden
sürecin nasıl işlediğini özetleyeceğiz.

### Senaryo

Senaryomuz şu şekilde gelişiyor:

- Gökhan isimli geliştirici `gdemir` isimli kendi [GitHub hesabında][gdemir]
  `uzem` adında bir [proje][proje] oluşturuyor.  Örneğin projeye aşağıdaki
  adresten erişebildiğini kabul edelim:
  
  [http://github.com/gdemir/uzem](http://github.com/gdemir/uzem)

- [GitHub hesap][roktas] adı `roktas` olan Roktas isimli geliştirici bir
  aşamada projeye dahil olarak Gökhan ile birlikte çalışmaya başlıyor.

### Roktas proje üzerinde çalışmaya nasıl başlamalı?

Projeyi oluşturan kişi Gökhan olduğuna göre Roktas öncelikle `uzem` isimli
projeyi Gökhan'ın deposundan "fork" ederek almalı.  Bu "fork" işlemi (ve
devamı) GitHub'ın [yardım sayfasında](http://help.github.com/forking/)
özetlenmiş.  Buna göre:

- Roktas Gökhan'ın hesabındaki [proje][proje] sayfasına giriyor.

- Proje sayfasında görülen "Fork" [butonuna][forkbuton] tıklayarak projeyi
  kendi hesabına klonluyor.  Artık Roktas'ın hesabında `uzem` isimli bir
  [depo][fork] var.

- Roktas GitHub üzerinde oluşturduğu bu yeni depoyu makinesine alıyor:

        roktas$ git clone git@github.com:roktas/uzem.git

- Roktas, kendi kopyası üzerinde çalıştığı esnada Gökhan'ın yaptığı yeni
  değişiklikleri takip etmek için deposunda örneğin `upstream` isimli bir dal
  oluşturarak bunu ilkliyor:

        roktas$ git remote add upstream git://github.com/gdemir/uzem.git
        roktas$ git fetch upstream

- Roktas proje üzerinde bilinen şekilde çalışıyor.  Yani kodlama yapıyor,
  değişikliklerini kaydediyor ve GitHub'taki deposuna gönderiyor:

        roktas$ ...
        roktas$ git commit -a -m "falan düzeltme yapıldı"
        roktas$ git push origin master

### Roktas projede yaptığı değişiklikleri Gökhan'a nasıl göndermeli?

Roktas'ın elindeki kopya GitHub'ın "fork" özelliğiyle Gökhan'ın kopyasından
türetildiğinden, GitHub Roktas'a yaptığı değişiklikleri Gökhan'a iletmek için
"Pull Request" adında bir kolaylık sunuyor.  Buna göre:

- Roktas kendi [proje][fork] sayfasına girerek "Pull Request"
  [butonuna][pullrequestbuton] tıklıyor.

- Açılan ileti penceresindeki leti alanına uygun bir açıklama yazdıktan sonra
  Gökhan'a ve isteğe bağlı olarak diğer alıcılara "yaptığım değişiklikleri
  kendi deponuza alın" isteğinde bulunuyor.

- Bu isteği alan Gökhan istekte belirtilen açıklamalara uygun şekilde
  Roktas'ın değişikliklerini kendi kopyasına uyguluyor.

### Roktas Gökhan'ın değişikliklerini nasıl takip etmeli?

Roktas proje üzerinde çalışırken Gökhan da kendi kopyası üzerinde bazı
değişiklikler yapıyor olabilir.  Roktas bu değişiklikleri şöyle almalı:

- Roktas kendi kopyasını hazırlarken oluşturduğu `upstream` dalını kullanarak
  Gökhan'daki değişiklikleri indiriyor:

        roktas$ git fetch upstream

- İndirilen değişiklikleri kendi kopyasıyla birleştiriyor:

        roktas$ git merge upstream/master

[gdemir]: http://github.com/gdemir/
[roktas]: http://github.com/roktas/
[proje]:  http://github.com/gdemir/uzem
[forkbuton]:  http://github.com/gdemir/uzem/fork/
[pullrequestbuton]:  http://github.com/roktas/uzem/pull_request/
[fork]:   http://github.com/roktas/uzem
