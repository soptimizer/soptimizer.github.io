---
layout: post
title: Windows Servis Geliştirme ve Nssm
date: 2021-07-16 00:00:00 +0300
description: #You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: service.jpg # Add image post (optional)
tags: [windows, servis, sunucu, nssm] # add tag
---

Servisler yazılım dünyasının vazgeçilmezleridir. Hangi işletim sisteminde olursa olsun servis kullanımı zorunlu ve itina ile gerçekleştirilmelidir.

Özellikle servis geliştirme noktasında yaşanan bazı noktaları kabaca değinmek istedim.

Önce şu altın kural ile başlamak lazım geliştirdiğiniz her console uygulaması bir servis olarak kullanılamaz. Servis geliştirmek istiyorsanız servisleri yönetecek sistem ile koordine olabilecek bir yapınız olması gerekir.

Bu amaçla visual studio'da aşağıdaki gibi bir windows service projesi oluşturabilirsiniz.

![image tooltip here](/assets/img/windows_service.jpeg)


Bu projeler windows servis yöneticisinin ihtiyacı olduğu fonksiyonları şablon olarak sapla ve destekler. Mesela OnStart, OnStop gibi yönetilebilir ve düzenlenebilir altyapıları mevcuttur. Bu C, C++, C# ve diğer diller içinde benzer şekildedir. Öyle ki Python gibi bir script dili için bile windows tarafında "win32serviceutil", "win32service", "win32event", "servicemanager" gibi bu işin yürütülmesini sağlayan kütüphaneler mevcuttur.

Buraya kadar sıkıntı yok ama ben bununla uğraşamam elimde kaynak kodu yok, sadece exe'si var diyebilirsiniz. Bu noktada işin içine NSSM giriyor. En kısa ifadeyle windows üzerinde standart console uygulamalarınızı servis olarak sorunsuz çalıştırmanıza yarayan bir "WRAPPER" olarak düşünebilirsiniz. Bu sayede ihtiyaç olmasına rağmen elinizdeki exe'nin desteklemediği OnStart, OnStop gibi yönetim fonksiyonları nssm üzerinden çözülerek servis çalıştırılır. Aslında çalışan NSSM'dir. NSSM bir watchdog gibi sizin ona verdiğiniz uygulamayı çalıştırır, kontrol eder ve yönetir.

Bu çocu zaman iş görür. Ancak bazı spesifik durumlarda sorunlar yaşayabilirsiniz.

Örnek olarak diyelim ki çalıştırdığınız uygulama windows tarafından gönderilen bazı sinyallere göre işlem yapacak. Misal bu sinyallere SIGTERM, SIGKILL olsun. Uygulamayı kapatırken bu sinyalleri işleyip ona göre bazı kaynak yönetim süreçlerini yürütebilirsiniz. Ve uygulamayı debug ettiğinizde hiç bir sorun yaşamayacaksınız. Ta ki NSSM ile servis olarak çalıştırana kadar. Çünkü NSSM uygulamayı sizin istediğiniz ve ya yakalayabileceğiniz sinyallerle kapatmayabilir. Sinyallerle çalışmak zaten sıkıntılıyken bir de bu işin içine girdiğinde servisim neden düzgün kapanmıyor sorununun içinde bulabilirsiniz kendinizi.

Daha detaylı bir örneği daha sonra paylaşacağım ama biraz teknikten uzak kalsak da olabildiğince net açıklamaya çalıştım.