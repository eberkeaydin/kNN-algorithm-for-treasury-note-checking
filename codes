import math

print("************ TREASURY NOTE TESTER PROGRAM WITH USING TREASURY ATTRIBUTE DATA SET AND INPUT NOTE ATTRIBUTES ***********")
k_value = int(input("Enter the 'k' value for kNN Method : "))

variant = float(input("Enter the variant of treasury note : "))
coefficient = float(input("Enter the coefficient value of treasury note : "))
lowness = float(input("Enter the lowness value of treasury note : "))
entropy = float(input("Enter the entropy value of treasury note : "))

file = open("data_banknote_authentication.txt.txt")



data_list = file.readlines()
data_list_copy = []

def kNN(inputList, dataList) :            # kNN FONKSİYONU İLE İNPUT GİRDİSİ BANKNOT ÖZNİTELİKLERİ İLE VERİ SETİNDEKİ ÖZNİTELİKLERİ KNN YÖNTEMİ İLE İŞLEME ALIP UZAKLIKLARI BULDUK.
    toplam_x = x = w = 0

    for i in range(len(inputList)) :
        x = (float(inputList[i]) - float(dataList[i]))**2
        toplam_x += x
    w = math.sqrt(toplam_x)
    return w

for i in range(len(data_list)):   # VERİ SETİNİ VİRGÜLLERDEN TEMİZLEDİK VE KOPYA BİR LİSTEYE ATTIK. BU SAYEDE VERİ SETİ LİSTESİ ÜZERİNDE MANİPÜLASYON YAPABİLECEĞİZ.
    a = data_list[i].split(",")
    data_list_copy.append(a)

base_treasury_note = [variant, coefficient, lowness, entropy]

distances = []

for i in range(len(data_list)):            # UZAKLIKLARI HER BİR BANKNOTUN LİSTEDEKİ İNDEXİ İLE BİRLİKTE TUTTUK. BU SAYEDE EN YAKINDAKİ BANKNOTLARA ULAŞABİLECEĞİZ.
    distance = kNN(base_treasury_note, data_list_copy[i])
    distance_array = [distance,i]
    distances.append(distance_array)

distances.sort(key= lambda x: x[0])  # UZAKLIKLARI SIRALAYIP ERİŞİME AÇIK HALE GETİRDİK.


print("*******************************************")
print("TREASURY NOTES WITH SORTED WITH DISTANCES : ")
print(distances)     # SIRALANMIŞ UZAKLIK LİSTESİNİ BASTIRDIK.

fakes = reals = 0

close_distances = distances[0 : k_value]       #  GİRİLEN "K" DEĞERİNE GÖRE EN YAKIN UZAKLIKLAR BİR LİSTEYE ATANDI
print("----------  PROPERTIES OF 'K' NUMBER OF NEIGHBORS  ----------")
for i in range(k_value):
    print("----------------------------------------------------------------------")
    print(" NEIGHBOR TREASURY NOTES PROPERTIES (VARIANT, COEFFICIENT, LOWNESS, ENTROPY, TYPE)")
    for j in range(len(data_list_copy[0])):
        value = data_list_copy[close_distances[i][1]][j]      # KOMŞU BANKNOTLARI DAHA ÖNCE YARATTIĞIMIZ LİSTELERİ KULLANARAK BİR DEĞERE ATAYIP TABLO OLARAK BASTIRMAYA ÇALIŞTIK.
        print(value, end=" ")



    print("DISTANCE FROM INPUT TREASURY NOTE : " ,round(close_distances[i][0],5), sep=" ")  # KOMŞU BANKNOTUN UZAKLIĞINI YAZDIRDIK.( BUNUN İÇİN CLOSE_DISTANCES LİSTESİNE ERİŞTİK)
    print("----------------------------------------------------------------------------")

for i in range(k_value):

    if data_list_copy[close_distances[i][1]][4] == "0\n" :  # LİSTEDE TÜRÜ BELİRTEN İNDEX "0\N" OLDUĞU İÇİN BANKNOT TÜRÜNE BU ŞEKİLDE ULAŞTIK.
        fakes += 1
    else:
        reals += 1

if fakes > reals :
    print("INPUT TREASURY NOTE IS FAKE !")  # KARAR YAPILARIYLA SAHTE- GERÇEK OLDUĞUNA KARAR VERİLEN INPUTUN TÜRÜ YAZDIRILDI.

elif fakes == reals :
    if data_list_copy[distances[0][1]][4] == "0" :
        print("INPUT TREASURY NOTE IS FAKE !")
    else:
        print("INPUT TREASURY NOTE IS REAL")
else:
    print("INPUT TREASURY NOTE IS REAL")


print("--------------------------------------------")
print("********** DATA SET IS PRINTING **********")
for line in data_list :             # VERİ SETİ YAZDIRILDI.
    print(line)

print("***** DATA SET IS PRINTED, GO UP FOR RESULTS ******")
print("*************** TEST IS STARTING *******************")

test_data_array = data_list_copy[662 : 763] + data_list_copy[1273 : ]   # TEST VERİLERİ İÇİN VERİ LİSTELERİ KOPYALANIP SLICE EDİLDİ.
data_without_test = data_list_copy[0 : 662] + data_list_copy[763 : 1273]

test_k_value = int(input("ENTER 'K' VALUE FOR TEST : "))

test_distance = right_guesses = 0
test_distances = []
for i in range(len(test_data_array)):
    for j in range(len(data_without_test)) :
        test_distance = kNN(test_data_array[i], data_without_test[j])
        test_distance_array = [test_distance, j]
        test_distances.append(test_distance_array)

    test_distances.sort(key=lambda x: x[0])
    close_test_distances = test_distances[0:test_k_value]

    test_fakes = test_reals = 0

    for i in range(test_k_value):
        print("----------------------------------------------------------------------")

        for j in range(len(data_list_copy[0])):
            result = data_without_test[close_test_distances[i][1]][j]
            print(result,end=" ")

        if result == "0\n":
            test_fakes += 1
        if result == "1\n":
            test_reals += 1

        print("DISTANCE OF TEST TREASURY NOTE : ", round(close_test_distances[i][0], 5), sep=" ")


    type_of_test_treasury_note = ""

    if test_fakes > test_reals:
        type_of_test_treasury_note = "0\n"
    elif test_fakes == test_reals:
        type_of_test_treasury_note = data_without_test[close_test_distances[0][1]][4]
    else:
        type_of_test_treasury_note = "1\n"


    print("ESTIMATED TYPE OF TREASURY NOTE : ", type_of_test_treasury_note)

    if type_of_test_treasury_note == test_data_array[i][4] :
        right_guesses += 1


    test_distances = []
    print("*************************************************************")

print("SUCCESS RATE : ", round(right_guesses / len(test_data_array ) * 100,2))
print("*******************************************************************************************************************************")
print("PROGRAM BY : EMIN BERKE AYDIN")
print("*******************************************************************************************************************************")
