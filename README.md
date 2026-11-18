# PERFEKCJA CRM

Lekki CRM offline dla Perfekcja Detailing Wołomin. Aplikacja używa wyłącznie HTML, CSS, JavaScript, IndexedDB i Service Workera; nie zawiera analityki, trackerów ani zewnętrznych bibliotek.

## Uruchomienie do podglądu na komputerze

W katalogu projektu uruchom `python -m http.server 8000`, a następnie otwórz `http://localhost:8000`. Dane testowe nie są dodawane. Pliki IndexedDB należą do konkretnej przeglądarki i pochodzenia (origin).

## iPad mini 4: ograniczenie instalacji

Safari udostępnia Service Worker (potrzebny do cache offline) tylko w bezpiecznym kontekście HTTPS albo na `localhost`. `localhost` na iPadzie oznacza sam iPad, a nie komputer w tej samej sieci. Otworzenie pliku HTML z aplikacji Pliki nie zapewnia wymaganego kontekstu ani stabilnej bazy. Z tego powodu nie da się uczciwie obiecać instalacji PWA na iPadzie bez przynajmniej jednorazowego źródła HTTPS.

Najprostsza ścieżka bez stałego hostingu: opublikować te statyczne pliki na darmowym hostingu HTTPS na czas pierwszej instalacji, otworzyć adres w Safari na iPadzie, użyć Udostępnij → Dodaj do ekranu początkowego i uruchomić aplikację online raz, aby Service Worker zapisał pliki. Potem sprawdzić działanie po włączeniu trybu samolotowego. Aplikacja nie przesyła danych klientów na serwer; pochodzenie witryny służy wyłącznie dostarczeniu plików. Dane IndexedDB są przypisane do tego adresu i Safari. Nie usuwaj danych witryny ani aplikacji bez uprzedniej kopii JSON. Utrata lub wygaśnięcie domeny może uniemożliwić ponowne uruchomienie zapisanego PWA offline.

To rozwiązanie nie wymaga płatnej subskrypcji, ale jednorazowa publikacja HTTPS jest konieczna dla Service Workera. Na tym etapie nie wykonano publikacji ani testu na iPadOS 15.8.8.

## Kopie zapasowe

W zakładce Kopia zapasowa wybierz „Zrób kopię JSON”. W oknie zapisu Safari wybierz aplikację Pliki i zapisz plik w iCloud Drive lub innym bezpiecznym miejscu. Zrób kopię co najmniej co 7 dni. Import waliduje strukturę i pyta o potwierdzenie zastąpienia bieżącej bazy. Eksport CSV obejmuje klientów, liczbę wizyt i sumę ich kwot.

## Weryfikacja

- `node --check app.js` sprawdza składnię JavaScript.
- Testy operacyjne wymagające Safari IndexedDB, Service Workera, pobierania plików i instalacji należy wykonać na urządzeniu docelowym. Nie są one deklarowane jako zaliczone w tym środowisku.
