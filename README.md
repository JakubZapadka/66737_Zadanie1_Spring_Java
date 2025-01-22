# Opis działania aplikacji

**Spring** to framework Java, który ułatwia organizację projektu i zarządzanie jego strukturą w sposób uporządkowany i elastyczny. W naszej aplikacji zastosowaliśmy architekturę **MVC** (Model-View-Controller), co pozwala na oddzielenie logiki biznesowej od prezentacji i interakcji z użytkownikiem.

## Struktura aplikacji

1. **Model**:  
   Model w naszej aplikacji nie jest obecnie wykorzystywany, ale został przygotowany do implementacji w przyszłości (np. w zadaniu 2).

2. **View (Widok)**:  
   Pliki odpowiedzialne za wygląd aplikacji, takie jak **HTML**, **CSS** i inne zasoby, znajdują się w folderze `src/main/resources`. To właśnie te pliki definiują sposób wyświetlania aplikacji użytkownikowi.

3. **Controller (Kontroler)**:  
   Kontroler odpowiada za obsługę żądań użytkownika, decydując o tym, co ma zostać wyświetlone i jak zareagować na dane wejściowe, np. przekierowując użytkownika do odpowiednich plików HTML.

## Przebieg działania aplikacji

1. **Uruchomienie aplikacji**:  
   Aplikacja startuje poprzez plik `src/main/java/pl/edu/vistula/first_project_java_spring/FirstProjectJavaSpringApplication.java`. Jest to główny plik odpowiedzialny za inicjalizację aplikacji.

2. **Uruchomienie serwera Apache**:  
   Po uruchomieniu aplikacji, automatycznie startuje serwer Apache na porcie **8080** (localhost), który umożliwia dostęp do aplikacji przez przeglądarkę internetową.

3. **Mapowanie URL w kontrolerze**:  
   Po wpisaniu adresu URL w przeglądarkę, aplikacja sprawdza, czy odpowiadająca podstrona istnieje. Aby dodać nową podstronę, wystarczy zdefiniować ją w kontrolerze. Klasa kontrolera musi być oznaczona adnotacją **`@Controller`**, a Spring automatycznie połączy ją z aplikacją.

4. **Obsługa błędów**:  
   Jeśli podstrona nie istnieje, użytkownik zostaje przekierowany na stronę `/error`, gdzie może zobaczyć kod błędu. Jeśli strona `/error` nie została wcześniej zdefiniowana, pojawi się domyślna strona błędu.

5. **Zwracanie odpowiedzi**:  
   Aplikacja może zwrócić różne odpowiedzi, takie jak tekst lub plik HTML:

   - **Zwracanie tekstu**:  
     Aby zwrócić tekst, używamy adnotacji **`@ResponseBody`**:
     ```
     @ResponseBody
     public String hello() {
         return "Hello Vistula, in my first Spring controller.";
     }
     ```

   - **Zwracanie strony HTML**:  
     Jeśli aplikacja ma zwrócić stronę HTML, możemy przekazać parametry przez metodę **GET**. Wartość parametru `name` jest opcjonalna i jeśli nie jest podana, domyślnie przyjmuje wartość „World”:
     ```
     public String greeting(@RequestParam(name="name", required = false, defaultValue = "World") String name, Model model) {
         model.addAttribute("name", name);
         return "greeting";
     }
     ```

6. **Generowanie strony HTML**:  
   Po zażądaniu strony przez użytkownika, aplikacja odwołuje się do folderu `resources/templates`, gdzie znajduje odpowiedni plik HTML.

7. **Folder `static`**:  
   Do przechowywania plików statycznych, takich jak zdjęcia, filmy czy style CSS, używamy folderu **`static`**, z którego aplikacja czerpie zasoby w folderze **`templates`**.

8. **Folder `target`**:  
   Podczas uruchamiania aplikacji tworzony jest folder **`target`**, który zawiera pliki wynikowe procesu kompilacji (np. pliki JAR/WAR). Można go bezpiecznie usunąć, ponieważ zawartość tego folderu jest generowana na nowo podczas kolejnej kompilacji.
