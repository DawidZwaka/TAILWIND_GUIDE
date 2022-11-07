# Kompendium wiedzy o Tailwindzie

## Czym jest tailwind?
Tailwnd, jak sami twórcy go ją to "utility-first CSS framework", a to znaczy, że tailwind jest zbudowany z niskopoziomwych klas których nazwa odnosi się do ich przeznaczenia. W przeciwieństwie do bootstrapa, czy material ui, które udostępniają nam wysokopoziomowe klasy komponentów takie jak button, card, badage. Tailwind wprowadza malutike funkcjonalne klasy, z których możemy budować większe komponenty takie jak w wyżej wspomnianych bibliotekach.

Ja lubię patrzeć na tailwinda jako na bibliotekę, która jest bolączką na problemy ze zwyczajnym inline stylingiem to znaczy rozwiązuje jej wszystkie problemy.

## Jak zbudowana jest klasa w tailwindzie?
Konstrukcja klas w tailwindzie jest niezwykle prosta i jej najbardziej podstawowa budowa może składać się z wariantu składającego się z nazwy wariantu i znaku ":" po nim następującym oraz części odpowiedzialnej za stylowanie. 

Oto przykład klasy ustawiającej kolor tła na biały po wywołaniu eventu 'hover':
```html
    <div class="hover:bg-white"></div>
```
Jeśli jesteś zaznajomiony z CSS'em to powyższy kod powinien być dla ciebie bardzo intuicyjny ze względu na jego spore podobieństwo do właściwości CSS'a.

## Dlaczego tailwind jest taki potężny?
1. ### Warianty
   Tailwind oferuje nam zestaw wariantów, które pozwalają nam na użycie utiltiy classes w zależności od interesujących nas warunków. Ponadto możemy tworzyć własne warianty przez co jesteśmy w stanie rozszerzać funkcjonalność tailwinda pod nasze potrzeby. O to lista najbardziej przydatnych wariantów: 

   * Pseudo klasy takie jak :hover, :focus, :first-child ect. 
   ```scss 
   element:hover {
        color: white;
   }
    // w tailwindzie hover:text-white 

    element:focus {
        padding: 1rem;
    }
    // w tailwindzie focus:p-4 

    element:first-child {
        display: block;
    }
    // w tailwindzie first:block 
    ```
    * Pseudoelementy takie jak ::after, czy ::before 
    ```scss
    element::after {
        content: "hello world";
    }
    // w tailwindzie after:content-["hello world"] 
    
    element::before {
        margin-left: 1rem;
    }
    // w tailwindzie before:ml-4
    ```
    * Responsive design variant zawierający w sobie breakpointy takie jak: sm, md, lg, xl, 2xl
    ```html
    <div class="sm:text-[22px]"></div>
    // ten div będzie miał font size równy 22px dla ekranów powyżej breakpointa sm 
    ```
    * Variant "dark", który odpowiada za stylowanie przy włączonym dark mode
    ```html
    <div class="dark:bg-black"></div>
    // ten div będzie miał czarne tło jeśli włączymy dark mode 
    ```
2. ### Dyrektywy screen, apply, layer, theme
    Tailwind to nie tylko możliwość korzystania z gotowych utility classes przygotowanych przez jego twórców, ale również możliwość ich rozbudowania między innymi korzystając z CSS'a. Specjalnie dla tego przypadku dostaliśmy parę przydatnych dyrektyw:
    * Apply - pozwala dodawać utlity classes do danej klasy CSS'a.
    ```scss
        .example-class {
            @apply bg-white px-10;
        }
        //kod wejściowy

        .example-class {
            background-color: white;
            padding-left: 40px;
            padding-right: 40px;
        }
        //kod wyjściowy
    ```
    * Layer - pozwala dodać własną utility class, component lub nadpisać talwindowy base styling
    ```scss
        @layer component {
            .example-component {
                @apply mx-10 bg-white;
            }
        }
        // powyższy kod dodaje klasę "example-component", która aplikuje w sobie utitlity classes takie jak mx-10 oraz bg-white. Komponent ten jest w pełni zarządzalny przez tailwinda dlatego zawsze przy dodawaniu customowych klass w CSS'ie powinniśmy korzystać z tej dyrektywy.

        @layer utility {
            .subgrid {
                display: subgrid;
            }

            @variants hover {
                .subgrid {
                    display: grid;
                }
            }
        }
        // sposób na dodanie własnej utility class

        @layer base {
            a {
                color: black;
            }
        }
        // Dla nadpisywania bazowego stylowania elementów html'a powinniśmy skorzystać z dyrektywy @layer base
    ```
    * Screen - pozwala dodawać stylowanie dla poszczególnych breakpointów
    ```scss
        @screen sm {
            .example-class {
                @apply mx-10;
            }
        }
        // stylowanie dla breakpointu sm i wzwyż
    ```
    * Theme - przydatny w momencie gdy chcemy skorzystać z jakiejś zmiennej zapisanej w motywie tailwinda
    ```scss
        .example-class {
            height: calc(100vh - theme(spacing[12]));
        }
        // theme(spacing[12]) odnośni się do wartości spacingu równej 48px
    ```

3. ### Customizacja motywu poprzez tailwind.config.js
    Wraz z tailwindem dostajemy możliwość jego customizacji, czy też rozszerzania. Daje nam to pełną kontrolę nad tym z jakich wartości będzie korzystał nasz motyw między innymi w zakresie breakpointów, kolorów, fontów, spacingów, wybudowanych komponentów, czy z jakich zewnętrznych pluginów będzie korzystał. Więcej na temat edycji pliku tailwind.config.js i jakie daje on możliwości znajdziecie [tutaj](https://tailwindcss.com/docs/theme).

4. ### Pluginy
    Tailwind udostępnia nam intefejs dzięki, któremu dodawanie nowych funkcjonalności jest proste i przejrzyste. Temat jest na tyle rozległy, że pozwolę sobie w tym miejscu pozostawić [link](https://tailwindcss.com/docs/plugins) do dokumentacji, ale bardzo zachęcam do zapoznania się z tą lekturą, bo potrafi rozwiązać to wiele czychających na nas problemów w pracy z Tailwindem.
    
5. ### Klauzula important 
   Jak w czystym CSS tak i tutaj możemy używać klauzuli important, aby to osiągnąć wystarczy dodać '!' na początku utility class zaraz po ostatnim znaku ":"
   ```html
   <div class="group-hover:!font-bold"></div>
    // ta klasa będzie objęta klauzulą important
    ```

6. ### Niestandardowe wartości dla utility class
   W przypadku gdy potrzebujemy jednorazowo wpisać niestandardową wartość dla utility class możemy to bardzo łatwo zrobić podmieniając wartość w utility class za "[NIESTANDARDOWA WARTOŚĆ]" większość komponentów wspiera tą funkcjonalność
   ```html
    <div class="bg-[#444444]"></div>
    // ten div posiada background color równy #444444 
    ```

7. ### Tailwind sprząta po sobie
    Mogłoby się wydawać, że skoro tailwind posiada w sobie tak wiele malutkich klas, to używanie go musi być niesamowiecie obciążające dla czasu ładowania strony w przeglądarce. Otóż nic bardziej mylnego, tailwind posiada wszyty mechanizm skanowania wybranych przez nas plików source przez co jest w stanie wyłapać klasy, które zostały użyte w plikach source i w ten sposób przygotowuje plik końcowy zawierający utility classes, które odnalazł na etapie skanowania plików source. Co powoduje, że nasz produkcyjny plik CSS nie zawiera w sobie klas, które nie są przez nas używane.

## Przydatne narzędzia

#### **Node packages**
[Tailwind CSS Debug Screens 📱]("https://www.npmjs.com/package/tailwindcss-debug-screens") - Malutki plugin, który na bieżąco pokazuje aktywny breakpoint, przydatny przy pisaniu RWD.

#### **Pluginy VSC**
[Tailwind CSS IntelliSense]("https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss") - Plugin, który podpowiada nam na bieżąco utility classes, pozwala zajrzeć jaki kod wyjściowy generuje dana klasa oraz highlightuje potęcjalne bugi w naszym kodzie css i html

[Tailwind CSS Highlight]("https://marketplace.visualstudio.com/items?itemName=ellreka.tailwindcss-highlight") - Malutki plugin, który koloruje klasy w naszym kodzie html, dzięki czemu część utility class odpowiadająca wariantowi jest wyszczególniona, co poprawia ogólną czytelność kodu.

#### **Pluginy PhpStorm**
[Tailwind CSS](https://plugins.jetbrains.com/plugin/15321-tailwind-css) - JetBrainsowy odpowiednik wyżej omawianego pluginu Tailwind CSS IntelliSense dla VSC

## Tipy oraz złote zasady pisania w tailwindzie ;)
1. Staraj się traktować tailwinda jako inline styling na sterydach i ograniczaj korzystanie z CSS'a - w tym spisuje się najlepiej,
2. Dziel powtarzające się fragmenty kodu na osobne komponenty,
3. Jeśli już musisz napisać coś w css'ie zastanów się, czy nie można tego rozwiazać pisząc plugin do tailwinda,
4. Jeśli dalej musisz napisać coś w css'ie nie zapomnij o używaniu dyrektyw dostarczanych przez tailwinda tj. (screen, apply, layer),
5. Korzystaj z dyrektywy theme() w css'ie jeśli chcesz pobrać jakąś wartość zapisaną w configu tailwinda,
6. Układaj klasy w odpowiedniej kolejności tj. najpierw bez variantów, później z wariantami, a na końcu rwd i ewentualne varianty. Przykładowe poprawnie ułożone klas: 
```html 
<div class="flex flex-col hover:bg-black md:flex-row md:hover:bg-gray-100"></div>
```
        
7. Pamiętaj, że spacingi w tailiwndzie mnożą się razy 4 to znaczy p-3 to tak naprawdę padding równy 12px bo 3*4 = 12 (Dla global font size równe 16px),
8. Jeśli dobrze znasz css'a to utility classes powinny być dla ciebie bardzo intuicyjne, bo tak naprawdę bardzo przypominają zwyczajne właściwości css'a, ale dla łatwiejszego developmentu zainstaluj w swoim IDE plugin do podpowiadania utiltiy class'es, bo przecież po co to wszystko pamiętać, czy przeszukiwać dokumentację co pięć sekund ;)
9. Elementy w js chwytaj za pomocą custom atrybutów lub data atrybutów. używanie do tego klas może być trochę mniej przejrzyste,
10. Jeśli chcesz zmienić zachowanie poszczególnych utility classes, pamiętaj o konfiguracji motywu w tailwind.config.js,
11.  Kompilator tailwinda, skanuje pliki wejściowe w poszukiwaniu utility classes, więc pamiętaj o odpowiednim ustawieniu do nich ścieżki w tailwind.config.js,
12. Naucz się <a href="https://alpinejs.dev/">Alpine.js</a> - dla aplikacji renderowanych po stronie serwera jest to idealny framework, którym zakodujesz proste funkcjonalności, a przy tym będziesz zachwycony jak świetnie współpracuje z tailwindem.

## Przydatne materiały
* https://www.youtube.com/watch?v=lZp4salRFFc
* https://www.udemy.com/course/tailwind-css-mastery/
* https://www.youtube.com/watch?v=mr15Xzb1Ook
* https://www.youtube.com/watch?v=pfaSUYaSgRo
