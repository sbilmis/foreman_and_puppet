    :Author: sbilmis

.. contents::



.. _trubada-vnc-ile-kullanıcı-arayüzlerine-görsel-bağlantı:

1 **TRUBA'da VNC ile kullanıcı arayüzlerine görsel bağlantı**
-------------------------------------------------------------

Kullanıcı arayüzü sunucularında (sardalya1 ve barbun1) vncserver kuruludur. Kullanıcılar aşağıdaki ayarları gerçekleştirdikten sonra kişisel bilgisayarlarında vncviewer kullanarak grafik arayüzü gerektiren programları  (MATLAB vb.) çalıştırabilir. 


.. warning::

    levrek1 sunucusunda vncserver kurulu değildir. 

- Öncelikle (SSH kullanılarak) arayüz makinesine bağlanılırak  kullanıcı hesabınızda bir VNC oturumu oluşturulur. Bu aşamada bir VNC parolasınının da belirlenmesi de gerekecektir.

Aşağıdaki örnek kampüs dışından bağlantı gerçekleştirdirildiği varsayılarak barbun1 sunucusu için yazılmıştır. Sunuculara nasıl bağlanılacağı hakkında `buradan <https://docs.truba.gov.tr/TRUBA/kullanici-el-kitabi/open-vpn/openvpn_info.html>`_ bilgi edinebilirsiniz. 

::

    ## barbun1 arayüz makinesine baglanmak için 
    ssh username@172.16.11.1
    vncpasswd
    ## (olusturacaginiz sifre TRUBA'ya bağlandığınız şifreden farklı olabilir)
    ## "view only password" seçeneği sorulduğunda "no" seçeneği ile devam ediniz. 

.. image:: ./vnc1.png

Parola oluşturulduktan sonra bir vnc oturumunun başlatılması gerekir.

::

    ## belirli bir ekran boyutuyla vnc oturumunu başlatın 
    vncserver -geometry 1440x900

.. image:: ./vnc2.png

Mevcut vnc oturumlarını listelemek ve ``X DISPLAY`` numarasını görmek için

::

    ## mevcut vncserver oturumlarını görmek için
    vncserver -list

.. image:: ./vnc3.png

Bu aşamadan sonra, **kişisel bilgisayarınızdaki herhangi bir VNC istemcisini kullanarak**, (örneğin `tigerVNC <https://tigervnc.org/>`_  ya da `turboVNC <https://sourceforge.net/projects/turbovnc/>`_ yazılımları) oturum oluşturduğunuz kullanıcı arayüzü sunucusuna belirlemiş olduğunuz şifreyle görsel bağlantı gerçekleştirebilirsiniz.

.. note::

    VNC bağlantısı yaparken IP adresinin sonuna getirilecek "X DISPLAY" numarası buradaki örnekten farklılık gösterebilir.


::

    ## terminal komutu ile (kendi bilgisayaranizdan)
    vncviewer 172.16.11.1:3
    ## bu aşamada oluşturmuş olduğunuz vnc şifresini girip masaüstüne erişim sağlayabilirsiniz. 

.. image:: ./vnc3_5.png

**tiger vnc-viewer** kullanıyorsanız eğer aşağıdaki gibi vnc sunucu bilgi kısmına IP numarası ve XDisplay numarasını yazarak da bağlanabilirsiniz. 

.. image:: ./vnc4.png

**turbovnc** kullanıyorsanız eğer aşağıdaki gibi vnc sunucu bilgi kısmına IP numarası ve XDisplay numarasını yazarak da bağlanabilirsiniz. 

.. image:: ./vnc6.png

1.1 Ek Notlar:
~~~~~~~~~~~~~~

- Hangi sunucuda VNC oturumu oluşturduysanız (barbun1 ya da sardalya1) sadece o sunucuya VNC ile bağlanabilirsiniz.

- VNC oturumu oluşturulduktan sonra, aynı oturum tekrar tekrar kullanılabilir. Her seferinde yeni parola ya da yeni oturum oluşturmaya gerek yoktur.

- VNC bağlantısında sorun yaşandığında önceki oturumlarınızı silerek yeni bir oturum oluşturmayı deneyebilirsiniz.


::

    ## vnc-server oluşturmuş olduğunuz sunucuya baglanin (örnegin barbun1)
      ssh username@172.16.11.1

    ## Mevcut VNC oturumlarını listeleyin
      vncserver -list

    ## Mevcut vnc oturumunu sonlandırin (X-DISPLAY numaranız farklı olabilir)\\
      vncserver -kill :3

.. image:: ./vnc5.png

.. note::

    VNC bilgileri ve logları ev dizininde ``.vnc`` dizininde tutulmaktadır. Herhangi bir sorunda bu dizini silip yeniden oluşturabilirsiniz.

::

    rm -rf ~/.vnc
