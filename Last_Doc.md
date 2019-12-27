Web tabanlı sunucu istemci mimarilerinde veri güvenliği genellikle istemci tarafında kullandığınız uygulamanın SSL katmanı üzerinden sağlanır.

Fakat istemcinin yapısı gereği SSL kullanamıyor ya da kullanmak istemiyor olabilirsiniz. Peki bu durumda ne yapabilirsiniz?

Aslında bunun için SSL'den kopya çekebiliriz. SSL en temelde Private/Public yani Gizli/Açık anahtarlar ile "Diffie-Hellman" metodolojisini kullanır.

Kısaca açıklamak gerekirse habeleşme için bağlantı kurulacağı zaman istemci ve sunucu kendi gizli ve açık anahtarlarını oluşturur. Karşılıklı olarak birbirleri ile açık anahtarlarını paylaşırlar. 
