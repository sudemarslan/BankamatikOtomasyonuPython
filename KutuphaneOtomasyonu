musteri_bilgileri={}
hesapnolari=set()
def veriyukle():#her fonksiyonda kod tekrarını önlemek için
    global musteri_bilgileri,hesapnolari
    musteri_bilgileri = {}#her calistiginda guncellemek istedigimiz icin buraya da yazdik
    hesapnolari = set()
    try:
        with open("24100011061.txt", "r", encoding="utf-8") as file:
            for satir in file:
                if "--" not in satir:
                    continue
                parcalar = satir.strip().split("--")
                if len(parcalar) == 2:
                    try:
                        hesap_no = int(parcalar[0].strip())
                        ad, soyad, bakiye = parcalar[1].strip().split()
                        musteri_bilgileri[hesap_no] = {
                            'ad': ad,
                            'soyad': soyad,
                            'bakiye': int(bakiye)
                        }
                        hesapnolari.add(hesap_no)
                    except ValueError:
                        continue
    except FileNotFoundError:
        print("dosya bulunamadi")


def veri_kaydet():#verilerin guncel durumlarini kaydetmek için kullanılır.fonksiyonlarda çağrısı yapılmalı
    with open("24100011061.txt","w",encoding="utf-8") as file:
        file.write("---MUSTERİ BİLGİLERİ---\n")
        for hesap_no,bilgiler in musteri_bilgileri.items():
            file.write(f"{hesap_no}--{bilgiler['ad']} {bilgiler['soyad']} {bilgiler['bakiye']}\n")


def ekleme():
    veriyukle()
    global musteri_bilgileri,hesapnolari
    try:
        sayi = int(input("Kac musteri girilecek:"))
    except ValueError:
        print("Lutfen gecerli sayi girin!")
        return
    for i in range(sayi):
        try:
            hesap_no = int(input(f"{i + 1}.Hesap numarasi:"))
            if hesap_no in hesapnolari:
                print("Bu hesap numarasi zaten bulunmakta!\n")
                continue
        except ValueError:
            print("Hesap numarasi sayisal veriden olusmali!")
            continue
        ad = input(f"{i + 1}.Musteri adi:")
        soyad = input(f"{i + 1}.Musteri soyadi:")
        try:
            bakiye = int(input(f"{i + 1}.Musteri bakiyesi:"))
        except ValueError:
            print("Bakiye bilgisi sayisal verilerden olusmali!\n")
            continue
        musteri_bilgileri[hesap_no] = {
            'ad': ad,
            'soyad': soyad,
            'bakiye': bakiye
        }
        hesapnolari.add(hesap_no)
    veri_kaydet()


def guncelleme():
    veriyukle()
    global musteri_bilgileri,hesapnolari
    yeni={}
    try:
        hesap = int(input("Guncellenecek hesabin hesap numarasi:"))
        if hesap not in hesapnolari:
             print("Bu hesap numarasina ait hesap bulunmamakta")
             return
    except ValueError:
         print("Hesap numarasi bilgisi sayisal veriden olusmali!")
         return
    print("Guncellenmek istenen musteriye ait musteri bilgileri:")
    mevcut=musteri_bilgileri[hesap]
    print(f"AD:{mevcut['ad']} SOYAD:{mevcut['soyad']} BAKİYE:{mevcut['bakiye']}\n")
    try:
        try:
            guncel_hesapno = int(input("Guncel hesap no:"))
            if guncel_hesapno!=hesap and guncel_hesapno in hesapnolari:
                print("Bu hesap numarasina sahip baska bir musteri bulunmaktadir!")
                return
        except ValueError:
            print("hesap numarasi sayisal veri olmali")
            return
        guncel_ad = input("Guncel ad:")
        guncel_soyad = input("Guncel soyad:")
        guncel_bakiye = int(input("Guncel bakiye:"))
    except ValueError:
        print("Bakiye bilgisi sayisal veri olmali!")
        return
    for hesapno,bilgiler in musteri_bilgileri.items():
        if hesapno!=hesap:
            yeni[hesapno] = bilgiler
    yeni[guncel_hesapno]={
        'ad':guncel_ad,
        'soyad':guncel_soyad,
        'bakiye':guncel_bakiye
    }
    hesapnolari.add(guncel_hesapno)
    musteri_bilgileri=yeni
    veri_kaydet()


def arama():
    global musteri_bilgileri,hesapnolari
    veriyukle()
    try:
        aranan=int(input("Aramak istediginiz musterinin hesap numarasi:"))
        if aranan not in hesapnolari:
            print("Boyle bir musteri bulunmamakta!")
            return
    except ValueError:
        print("Hesap numarasi sayisal veriden olusmali!")
        return
    mevcut=musteri_bilgileri[aranan]
    print("Aradiginiz mustreiye ait bilgiler:")
    print(f"AD:{mevcut['ad']} SOYAD:{mevcut['soyad']} BAKİYE:{mevcut['bakiye']}\n")


def parayatirma():
    global musteri_bilgileri,hesapnolari
    veriyukle()
    try:
        hesap=int(input("Para yatirilacak hesabin hesap numarasi:"))
        if hesap not in hesapnolari:
            print("Bu hesap numarasina ait musteri bulunmamakta\n")
            return
    except ValueError:
        print("Hesap numarasi sayisal veriden olusmali")
        return
    mevcut=musteri_bilgileri[hesap]
    print("Para yatirilacak musteriye ait bilgiler:")
    print(f"AD:{mevcut['ad']} SOYAD:{mevcut['soyad']} BAKİYE:{mevcut['bakiye']}\n")
    try:
        miktar=int(input("Yatirilmak istenen miktari giriniz:"))
        if miktar<0:
            print("Yatirilmak istenen miktar 0'dan buyuk olmali!")
            return
    except ValueError:
        print("Yatirilmak istenen miktar sayisal veriden olusmalidir")
        return
    mevcut['bakiye']+=miktar
    print(f"Para yatirildiktan sonraki bakiye:{mevcut['bakiye']}")
    veri_kaydet()


def paracekme():
    global musteri_bilgileri, hesapnolari
    veriyukle()
    try:
        hesap = int(input("Para cekilecek hesabin hesap numarasi:"))
        if hesap not in hesapnolari:
            print("Bu hesap numarasina ait musteri bulunmamakta")
            return
    except ValueError:
        print("Hesap numarasi sayisal veriden olusmali")
        return
    mevcut = musteri_bilgileri[hesap]
    print("Para cekilecek mustreiye ait bilgiler:")
    print(f"AD:{mevcut['ad']} SOYAD:{mevcut['soyad']} BAKİYE:{mevcut['bakiye']}\n")
    try:
        miktar = int(input("Cekilmek istenen miktari giriniz:"))
        if miktar < 0:
            print("Cekilmek istenen miktar 0'dan buyuk olmali!")
            return
    except ValueError:
        print("Cekilmek istenen miktar sayisal veriden olusmalidir")
        return
    if miktar>mevcut['bakiye']:
        print("Yetersiz bakiye!")
    else:
        mevcut['bakiye'] -= miktar
    print(f"Para cekildikten sonraki bakiye:{mevcut['bakiye']}")
    veri_kaydet()


def faturaodeme():
    global musteri_bilgileri,hesapnolari
    def faturahesapla():
        kWh=2.59
        liste1=['nisan','haziran','eylul','kasim']#30
        liste2=['ocak','mart','mayis','temmuz','agustos','ekim','aralik']#31
        liste3 = ['subat']  # 29
        try:
            hesap = int(input("Fatura odemesi yapacak olan musterinin hesap numarasi:"))
            if hesap not in hesapnolari:
                print("Bu hesap numarasina ait musteri bulunmamakta!\n")
                return
        except ValueError:
            print("Hesap numarasi sayisal deger olmali!")
            return
        ay=input("Odemesi yapilacak olan ayi giriniz:")
        if ay in liste1:
            kullanim=int(input("Aylik elektrik tuketiminizi saat cinsinden yaziniz:"))
            miktar=30*kullanim*kWh
        elif  ay in liste2:
            kullanim = int(input("Aylik elektrik tuketiminizi saat cinsinden yaziniz:"))
            miktar = 31 * kullanim * kWh
        elif ay in liste3:
            kullanim = int(input("Aylik elektrik tuketiminizi saat cinsinden yaziniz:"))
            miktar = 29 * kullanim * kWh
        else:
            print("Gecersiz ay girdiniz!")
            return
        mevcut=musteri_bilgileri[hesap]['bakiye']
        if miktar>mevcut:
            print("Yetersiz bakiye")
            print(f"Fatura tutari:{miktar:.2f} bakiyeniz:{mevcut}")
        else:
            musteri_bilgileri[hesap]['bakiye']-=miktar
            print(f"Fatura odemesi yapildi.Yeni bakiye:{musteri_bilgileri[hesap]['bakiye']:.2f}")
            veri_kaydet()
    faturahesapla()


def paratransferi():
    veriyukle()
    global musteri_bilgileri,hesapnolari
    try:
        gonderen = int(input("Parayi gonderecek olan hesabin hesap numarasi:"))
        if gonderen not in hesapnolari:
            print("Gonderen hesap numarasina ait musteri bulunmamakta!")
            return
    except ValueError:
        print("Hesap no sayisal veriden olusmali!")
        return
    try:
        alici = int(input("Alici olan hesabin hesap numarasi:"))
        if alici not in hesapnolari:
            print("Alici hesap numarasina ait musteri bulunmamakta!")
            return
    except ValueError:
        print("Hesap numarasi sayisal veriden olusmali!")
        return
    print("Gonderen hesaba ait bilgiler:")
    mevcut1=musteri_bilgileri[gonderen]
    print(f"AD:{mevcut1['ad']} SOYAD:{mevcut1['soyad']} BAKİYE:{mevcut1['bakiye']}\n")
    print("Alici hesaba ait bilgiler:")
    mevcut2 = musteri_bilgileri[alici]
    print(f"AD:{mevcut2['ad']} SOYAD:{mevcut2['soyad']} BAKİYE:{mevcut2['bakiye']}\n")
    miktar=int(input("Gonderilmek istenen miktari giriniz:"))
    if miktar<0:
        print("Gonderilmek istenen miktar 0'dan buyuk olmali!")
    else:
        if miktar>mevcut1['bakiye']:
            print("Yetersiz bakiye")
        else:
            mevcut1['bakiye']-=miktar
            mevcut2['bakiye']+=miktar
    print("Para transferi gerceklestikten sonraki hesaplarin bakiye durumu:")
    print(f"Gonderen hesaba ait bakiye:{mevcut1['bakiye']}")
    print(f"Alici hesaba ait bakiye:{mevcut2['bakiye']}")
    veri_kaydet()


def silme():
    global musteri_bilgileri, hesapnolari
    veriyukle()
    yeni={}#silinmeyecekler icin
    yeni_kume=set()#silinmeyecekler icin
    try:
        hesap=int(input("Silinecek musteriye ait hesap numarasi:"))
        if hesap not in musteri_bilgileri:
            print("Bu hesap numarasina ait musteri bulunmamakta!")
            return
    except ValueError:
        print("Hesap no sayisal veriden olusmali!")
        return
    for hesapno,bilgiler in musteri_bilgileri.items():
        if hesapno!=hesap:
            yeni[hesapno]=bilgiler
    for hesapno in musteri_bilgileri:
        if hesapno!=hesap:
            bilgiler=musteri_bilgileri[hesapno]
            yeni[hesapno]={
                'ad':bilgiler['ad'],
                'soyad':bilgiler['soyad'],
                'bakiye':bilgiler['bakiye']
            }
            yeni_kume.add(hesapno)
    print("Musteri silindi")
    musteri_bilgileri=yeni
    hesapnolari=yeni_kume
    veri_kaydet()


def anamenu():
    veriyukle()
    print("---BANKAMATİK OTOMASYONU---")
    while True:
        try:
            secim = input("\nYapilmak istenen islemi seciniz:\n1-Ekleme\n2-Guncelleme\n3-Arama\n4-para yatirma\n5-Para cekme\n6-Fatura odeme\n7-Para transferi\n8-silme\n9-cikis\n")
            secim=int(secim)
            if  secim<1 or secim>9:
                print("Gecersiz giris\n")
                continue
        except ValueError:
            print("Gecerli giris yapin")
            continue
        if secim == 1:
                ekleme()
        elif secim == 2:
                guncelleme()
        elif secim == 3:
                arama()
        elif secim == 4:
                parayatirma()
        elif secim == 5:
                paracekme()
        elif secim == 6:
                faturaodeme()
        elif secim == 7:
                paratransferi()
        elif secim == 8:
                silme()
        elif secim == 9:
            break
anamenu()
