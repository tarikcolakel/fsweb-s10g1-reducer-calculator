# The Reducer Pattern Modül Projesi: Hesap Makinası

Bu hafta reducer yaklaşımını incelediniz. Bu projede bugün öğrendiklerimizi pekiştireceğiz.

## Giriş

- Bu projede, sayıları herhangi bir sırayla toplayabilen, çarpabilen, çıkarabilen ve çıkartabilen, ayrıca hafızaya kaydetme ve callback özellikleri ekleyebilen basit bir hesap makinesi uygulaması oluşturacaksınız.
- Koda eksik parçaları ekleyerek başlayacak ve UI, reducer ve event dosyalarında sıfırdan özellikler oluşturarak projeyi tamamlayacaksınız.
- **Bu hesap makinesi bildiklerimizden biraz farklı. Her yeni hesaplamasında önceki hesabın sonucunu ve yeni bir sayıyı parametre olarak alıyor.** İşlem sonunda hesap makineniz aşağıdaki gibi çalışmalıdır:

![Hesap Makinası Örnek](proje-hedefi.gif)

**_Görevlerinizi tek tek tamamladığınızdan ve ilerlemeden önce her bir görevi test ettiğinizden emin olun.._**

## Talimatlar

### Görev 1: Proje Kurulumu

- [ ] Forklayın
- [ ] Klonlayın
- [ ] Ana dizine gidin
- [ ] `npm install`
- [ ] `npm start`

### Görev 2: Proje Gereksinimleri

#### Reducer'ı bağlayın

> _Kullanıcı arayüzümüzü reducera ve ilk state'e bağlayarak sürecimize başlayalım.._

- [ ] Uygulama klasöründe gezinin, özellikle "App.js", "/reducer/index.js" ve "/actions/index.js" dosyaları.
- [ ] `TotalDisplay` bileşeni bir değer alır ve bu değeri stillenmiş bir textarea'da gösterir. BU BİLEŞENİ DEĞİŞTİRMENİZE GEREK YOK.
- [ ] `CalcButton` bileşeni bir `onClick` metodu ve bir değer alır, bu değeri görüntüler ve `onClick` metodunu ui butonuna ekler. BU BİLEŞENİ DEĞİŞTİRMENİZE GEREK YOK.
- [ ] App.js içine, useReducer hookunu import edin, uygulamamızın reducer'ı ve initialState nesnesi buradan gelecek.
- [ ] Uygulama state'ine ve dispatch fonksiyonuna erişmek için useReducer hookunu kullanın.

#### State'i UI'de görüntülemek.

> _Artık App bileşenimizde state'e erişimimiz var (Bunu console.log ya da React dev tools'dan gözlemleyebilirsiniz). State'i örnek ekranımızdaki gibi render edelim._

- [ ] Operation elemanı içindeki "X" i `state.operation` ı referans alarak değiştirin.
- [ ] Memory elemanı içindeki "0" ı `state.memory` yi referans alarak değiştirin.
- [ ] TotalDisplay bileşenine değer atarken "0" ı `state.total` ı referans alarak değiştirin.
- [ ] UI'de initialState'teki değerlerle total, operation ve memory'yi kontrol edin (100, \* ve sırasıyla 100)
- [ ] Reducer'daki initialState değerini değiştirerek elde ettiğiniz state'i test edin:

```
export const initialState = {
  total: 0,
  operation: "+",
  memory: 0
}
```

- [ ] Ekranınızın state'teki değişikliği doğru bir şekilde yansıttığını kontrol edin.

#### Hazır action'ı bağlama.

> _Artık State'imizi görebildiğimize göre, kullanıcının bunu değiştirebilmesine izin verelim. Hazır bir action ile başlayalım... Total'ı bir artıralım._

- [ ] `ADD_ONE` action'ına (./reducer/index.js içindeki) ve `addOne` action oluşturucuya (./actions/index.js içindeki) göz atın. Bu action total'a 1 ekler.
- [ ] `addOne` action oluşturucuyu App.js içine import edin.
- [ ] `App.js` içinde bir event handler oluşturarak, 1 butonunun `onClick` metoduna ekleyin.
- [ ] Event handler içinde, `addOne` action oluşturucuyu dispatch edin.
- [ ] Eventinizin doğru çalışıp çalışmadığını tarayıcınızda 1 butonuna basarak test edin. Total'iniz 1 artmalı.
- [ ] Bir butona tıklandığında güncellenen totali nasıl gösterebileceğimizi düşünün. Hangi adımlar vardı? `soruyu-anlamak.md` dosyası içine, kendi cümlelerinizle tüm adımları yazın.

#### Daha iyi bir hazır action bağlayın.

> _Her sayı için ayrı action eklemek sıkıcı olabilir. TÜM sayısal girdiler için çalışabilecek bir action ekleyelim_

- [ ] `APPLY_NUMBER` action'a (./reducer/index.js içindeki) ve `applyNumber` action oluşturucuya (./actions/index.js içindeki) göz atalım. Bu action, action oluşturucuya iletilen bir sayıyı ekler, çarpar veya çıkarır.
- [ ] `applyNumber` action oluşturucusunu `App.js.` içine import edin
- [ ] Daha önce 1 butonuna eklediğimiz event handlerı silin ya da comment içerisine alın.
- [ ] Argüman olarak bir sayı alan ve `applyNumber` ı dispatch eden bir event handler oluşturun.
- [ ] Bu eventhandlerı, argümanına 1 vererek 1 butonunun onClick metod'una bağlayın. (Şunu unutmayın onClick metoduna bir fonksiyon aktarıyoruz, var olan bir fonksiyonu direk çalıştırmıyoruz(too many re-renders hatası alırız)
- [ ] 1 butonuna basıldığında totali 1 artırıp ekrana yazdırıp yazdırmadığını test edin.
- [ ] Yeni event handlerınızı gerekli değerleri vererek tek tek diğer butonlara da bağlayın.
- [ ] Tüm butonlara tek tek tıklandığında totale doğru değerleri ekleyip eklemediğini test edin.

#### Bir action oluşturucu oluşturun ve bağlayın.

> _Şu anda uygulamamız sadece toplama işlemi yapıyor. Şimdi bunu değiştireceğiz. Kendi action oluşturucunuzu yaratmanın vakti geldi!_

- [ ] `CHANGE_OPERATION` action'a (`./reducer/index.js` içinde) göz atın. Bu reducer operatör değeri alır (+,- ve \*) ve bunu state'e aktarır.
- [ ] Argümanı olarak bir operatör alan bir action oluşturucu oluşturun (`./actions/index.js` içinde) ve type'ı `CHANGE_OPERATION.` olan action nesnesi oluştursun.
- [ ] Yeni action oluşturucuyu `App.js` ye import edin.
- [ ] `+`, `-` ve `*` butonlarına tıklandığında, ilgili operatörü action oluşturucunuza ekleyen bir event handler oluşturun. Her buton için doğru operatörü gönderdiğinizden emin olun.
- [ ] Operatör butonlarının doğru şekilde çalıştığından ve sayıları doğru işleme(toplama, çıkarma v.b.) tabi tuttuğundan emin olmak için test yapın.

#### Bir reducer ve action oluşturucu oluşturun ve bağlayın.

> _Şimdi ekran görüntüleyiciyi sıfırlama özelliği ekleyeceğiz. Bunun için reducer ve action oluşturucunun tamamını kendiniz yapacaksınız._

- [ ] `./reducers/index,` içinde, `CLEAR_DISPLAY` case'i oluşturun. Bu case total değer statini 0 yapacak.
- [ ] `./actions/index,` içinde, action oluşturucuyu ve adı `CLEAR_DISPLAY` olan bir action constant'ını string değeri ile ekleyin. Reducer dosyanızda da bu sabit değeri import ettiğinizden emin olun.
- [ ] `App.js,` içinde clearDisplay action oluşturucuyu import edin.
- [ ] clearDisplay action oluşturucunuzu dispatch eden bir event handler yazın ve "CE" butonuna bağlayın.
- [ ] clearDisplay butonunuzun düzgün çalışıp çalışmadığını test edin.

#### Esnek olarak Memory fonksiyonları ekleyin.

> _Tebrikler! Tüm işlemler için actionler ekleme görevini başarıyla tamamladınız! Şimdi aynı işlemleri takip ederek yeni özellikler ekleyeceksiniz. Tüm caseler için bir sonraki case e geçmeden önce testlerini yapmayı unutmayın._

- [ ] `M+` a tıklandığında, şu anki memory değerine şu anki total değerini kaydetsin. UI'de test edin.
- [ ] `MR` a tıklandığında, şu an memorydeki değer şu anki total değerine aktarsın (APPLY_NUMBER case ine göz atın). UI'de test edin.
- [ ] `MC` e tıklandığında, şu anki memory değeri sıfırlasın. UI'de test edin.

### Görev 3: Esnek görevler

- [ ] Hesap makinesinin rakamlar ekleme yerine tek tek rakamları toplamaya odaklanan bir sürümü vardır. Total stateine bağımsız bir rakam eklemeyi nasıl düşünürsünüz?
- [ ] [Şurada bir örnek var](https://freshman.tech/calculator/) reducer olmayan bir javascript hesap makinası uygulaması. Yeni bir branch oluşturup hesap makinasının yeni versiyonunu buraya yükleyin.
