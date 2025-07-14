---
layout: post
title:  "Inżynieria oprogramowania i polityka"
date:   2025-07-14
categories: polityka
---
## Wprowadzenie

Zaczniemy na spokojnie od tematu, którego pewnie większośc z was nie kojarzy z inżynierią oprogramowania. Opowiem wam o polityce, a właściwie o tym, jak pewne praktyki wykorzystywane w inżynierii oprogramowania możemy połączyć z namysłem nad, a docelowo z kształtowaniem polityki publicznej.

Spokojnie, nie będzie nic o tym, jak big tech manipuluje naszymi umysłami, żebyśmy myśleli w taki a nie inny sposób i głosowali na tych, a nie innych kandydatów (przynajmniej nie tym razem). Nie będzie też o błazenskich technikach NLP, niech takie banialuki uprawiają kołczowie z innych portali.

Na poczatku musimy sobie powiedzieć, co to jest inżynieria oprogramowania. Spośród szeregu różnych definicji, mnie najbardziej podoba się ta autorstwa Iana Sommerville'a: 
> inżynieria oprogramowania jest dziedziną inżynierii obejmującą wszystkie aspekty produkcji oprogramowania - od wstępnej koncepcji po jego działanie i obsługę (konserwację).

Jedną z poddziedzin Inżynierii oprogramowania jest coś, co moglibyśmy określić mianem inżynierii wymagań. Ten sam Sommerville inżynierią wymagań określa jako
> proces prowadzący do zrozumienia i zdefiniowania usług wymaganych od systemu oraz zidentyfikowania ograniczeń narzucanych na działanie systemu i jego budowę.

Co ciekawe, podobnej definicji używają Dean Leffingwell i Don Widrig dla pojęcia *zarządzania wymaganiami*:
> systematyczne podejście do uzyskiwania, organizowania i dokumentowania wymagań systemu (...).

Jeśli pracujecie na budowie systemów IT, to pewnie zaobserwowaliście, że w tym momencie często zdefiniowanie wymagań ma formę tzw. *user story* (wierzcie lub nie, ale telefon zrobił mi autokorektę do pojęcia USSR story, co nawet nie byłoby takie głupie).

## User Story

User story ma strukturę: 
*As a (role, persona) I (want to), so that (something).*

User story nie jest głupie, naprawdę. User story niesie w sobie szereg istotnych wartości (i dla klienta, i dla nas, inżynierów oprogramowania):
1. Pozwala nam skupić się na potrzebie klienta
2. Prezentuje perspektywę biznesową abstrahując od warstwy systemowej,
3. Daje nam szybki przegląd ról naszych użytkowników i może być podstawą do zarządzania rolami i uprawnieniami w systemie (ale  z tym to ostrożnie).
Dodatkowo każde user story powinno być okraszone kryteriami akceptacji, które powiedzą nam, kiedy klient uzna, że wymaganie zostało zrealizowane. Te kryteria akceptacji mogą z kolei nam służyć jako wstęp do pisania scenariuszy testów - szczególnie, gdy skorzystamy z praktyk behavior-driven development.

User story spopularyzowane zostały przy wykorzystywaniu zwinnych praktyk tworzenia oprogramowania (a kto dziś nie tworzy oprogramowania zwinnie?). Tylko jedna ważna rzecz, o której często się zapomina: user story to nie wymagania. Pisanie user story to nie inżynieria wymagań. Jeśli pracujecie na budowie systemów IT, to pewnie o tym wiecie (i co z tego, ja też wiem, a byłem w takich projekach), jeśli nie, to pewnie nic was to nie obchodzi, co ten typ bredzi i gdzie ta cała polityka?

## 5 Whys

Zwinne wytwarzanie oprogramowania pełnymi garściami czerpie z filozofii lean. Taichii Ochno, jeden z twórców Toyota Production System opracował technikę zwaną dzisiaj 5 Whys (5 razy Dlaczego). Ta technika była wykorzystywania w procesach doskonalenia procesów produkcji i generalnie sprowadzała się do czegoś, co można by określić mianem techniki trzylatka. Każdy rodzic nieraz pewnie doświadczył tej techniki na własnej skórze, gdy dziecko niezaspokojone odpowiedzią rodzica zadaje kolejne pytania DLACZEGO? 

Możemy sobie wyobrazić przypadek systemu do zapisywania się do lekarza. Możemy trafić na user story w stylu "jako zalogowany klient chcę mieć możliwość wyboru specjalisty, aby móc się do niego zapisać".

Taki opis można potraktować jako proste wymaganie wyświetlania listy specjalistów, możemy sobie z klientem porozmawiać jeszcze o jakiejś paginacji, jeśli jest ich dużo czy wyświetlać od razu nazwiska, czy na razie tylko specjalizacje, albo co tam jeszcze. A później proste SELECT * FROM TABELA, JESTEM MISTRZEM SQL-a (mamy tutaj jakiegoś archeologa? Ja to usłyszałem u Mariusza Gila, ale twórcą tego grepsu jest chyba ktoś inny). 

Ale możemy też to wymaganie potraktować jako wstęp do rozmowy i drążyć, drążyć, drążyć, aż znajdziemy źródło wymagania. No bo przecież, po co mi lista specjalistów, jeśli wiem, do kogo potrzebuję się zapisać? Może wystarczy, żebym jako użytkownik dostał pole tekstowe, w które zacznę wpisywać endok..., a system sam podpowie mi resztę i pozwoli umówić wizytę u endokrynologa.

Możemy więc zapytać, dlaczego potrzebujemy funkcji wyboru specjalisty? Może się wtedy dowiemy, że chodzi nam o szybkość i prostotę (keep it simple, stupid), żeby użytkownik nie musiał nie wiadomo ile scrollować (ajajaj, wtedy może nam nie być na rękę, ani pełna lista, ani nawet paginacja). No więc możemy drążyć dalej: dlaczego ta prostota? Wtedy być może dowiemy się, że być może nie zawsze użytkownik wie, czego potrzebuje i zależy nam na tym, by mu ten wybór ułatwić (tutaj akurat lista może pomóc, ale niekoniecznie rozwiązuje problem "nie wiem, czego potrzebuję; czym w ogóle zajmuje się endokrynolog?"). 

Zadając kolejne pytania możemy dojść do wniosku, że zależy nam na tym, żeby na podstawie wskazanych symptomów *zasugerować* użytkownikowi potencjalnego specjalistę. Przechodząc przez 5 Whys możemy dojść do naszego wymagania źródłowego i odkryć, że to, czego chcemy w naszej aplikacji to nie lista specjalistów, ale pomoc w doborze odpowiednich specjalistów na podstawie opisu objawów pacjenta. 

I być może właśnie to powinniśmy implementować. Bo jeżeli robimy aplikację dla sieci placówek medycznych, to to jest właśnie nasz core business, tutaj powinniśmy szykować efekt wow. Uczy nas tego zarówno Business Model Canvas, jak i Domain-Driven Design.

## Dobra, dobra, nie pie\*ol, gdzie ta polityka?

Co jest analogią systemu informatycznego w naszej polityce? Państwo. Kto jest biznesem, kto jest klientem w naszym państwie? My, obywatele. Kto jest dostawcą oprogramowania? Politycy. Well, właściwie to administracja, ale to politycy są inżynierami wymagań w tej analogii. 

Problem w tym, że oni mają trudniej, niż inżynierowie wymagań w budowlance systemów IT. Trudniej, ponieważ nie mają listy wymagań, ani nawet user story. Oni trochę szyją. Szyją na podstawie badań (ta, jasne!), albo tego, co do nich dotrze z kółeczka adoratorów na śp. twitterze (prędzej) lub od projektantów contentu w osobach tzw. spin doctorów (był taki czas, że byli modni). 

Więc młucą. Młucą pomysły na prawo i lewo, często suflują jakieś pomysły mniej lub bardziej jawnie. Czasem produkują (projektują) problem pod swoje rozwiązanie, albo chociaż ramkują dyskusję tak, jak im wygodnie. 

Aż zażre. A jak zażre, to już będą się tego trzymać. Jak Polska w ruinie i 500 plus dziesięć lat temu (!!!). Jak uciskani przedsiębiorcy, prześladowani katolicy, czy co tam nam zażre w danej kampanii.

Weźmy sobie zagadnienie, o którym było głośno w niejednej kampanii: mieszkalnictwo. Ubierzmy to w formułę user story: *jako obywatel chcę mieć możliwość wzięcia taniego kredytu na zakup mieszkania, aby mieć gdzie mieszkać i nie wydawać połowy pensji na czynsz*. 

Teraz spróbujmy rozbić tę potrzebę w poszukiwaniu potrzeby źródłowej (root cause).

1. Dlaczego chcesz mieć możliwość wzięcia taniego kredytu na zakup mieszkania?
	Ponieważ chcę mieć własne mieszkanie, które jest tańsze w utrzymaniu niż wynajem.
2. Dlaczego chcesz mieć własne mieszkanie, które jest tańsze w utrzymaniu niż wynajem?
	Ponieważ wynajem jest niepewny, a koszty rosną, co utrudnia planowanie wydatków w dłuższym okresie.
3. Dlaczego wynajem jest niepewny i rosnące koszty utrudniają planowanie wydatków?
	Ponieważ właściciele mogą w dowolnym momencie podnieść czynsz lub wypowiedzieć umowę, co sprawia, że brakuje stabilności mieszkaniowej.
4. Dlaczego właściciele mają dużą swobodę w podnoszeniu czynszów i wypowiadaniu umów?
	Ponieważ brakuje regulacji, które chroniłyby najemców i wspierały stabilność rynku mieszkaniowego.
5. Dlaczego brakuje regulacji wspierających stabilność rynku mieszkaniowego?
	Ponieważ system mieszkaniowy nie zapewnia długoterminowych rozwiązań wspierających zarówno wynajem, jak i zakup mieszkań w przystępnych cenach.

Weryfikując wyartykułowaną potrzebę taniego kredytu mieszkaniowego możemy odkryć, że celem nie jest tani kredyt na mieszkanie, tylko stabilność mieszkaniowa i bezpieczeństwo finansowe. Tani kredyt nie jest jedyną możliwością zaspokojenia tej potrzeby. Prawdziwa potrzeba mogłaby być sformułowana jako user story o treści *jako obywatel chcę stabilnych i dostępnych rozwiązań mieszkaniowych, aby móc mieszkać bez obaw o nieprzwidywane koszty i brak stabilności*. 

To oczywiście też nie jest koniec pracy, w następnych krokach należałoby spisać potencjalne możliwości (tani kredyt, mieszkania na długoterminowy najem od jednostek samorządu terytorialnego, regulacja czynszów lub najmów od prywatnych właścicieli itp.), a następnie przeprowadzić OSR dla wskazanych rozwiązań i zdecydować się na to, które potencjalnie powinno przynieść największe korzyści dla klienta. Czyli ostatecznie dla nas wszystkich. 