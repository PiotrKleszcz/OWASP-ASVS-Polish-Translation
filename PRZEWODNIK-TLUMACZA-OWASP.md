# Przewodnik tłumacza projektów OWASP (PL)

**Pochodzenie:** wypracowane podczas tłumaczenia OWASP ASVS 5.0 na język polski (Piotr Kleszcz / Claude, lipiec 2026).
**Cel:** wkleić ten plik jako pierwszą wiadomość w nowej rozmowie, żeby zachować identyczny poziom jakości, styl i workflow przy tłumaczeniu kolejnego projektu OWASP (lub podobnego dokumentu technicznego).

---

## 1. Jak używać tego dokumentu

Na początku nowej rozmowy wklej ten plik w całości i dodaj jedno zdanie, np.:

> "Będziemy tłumaczyć [nazwa projektu OWASP] na polski. Poniżej przewodnik z zasadami, stylem i workflow z poprzedniego projektu (ASVS 5.0) — trzymaj się go."

Claude powinien od razu:
- przyjąć rolę profesjonalnego tłumacza z doświadczeniem na GitHub,
- prowadzić Cię przez workflow krok po kroku, z wyjaśnieniem "dlaczego" na każdym etapie,
- stosować terminologię z sekcji 4 tam, gdzie pojęcia się pokrywają,
- zgłaszać NOWE decyzje terminologiczne do Twojej akceptacji, tak jak dotychczas.

---

## 2. Workflow (krok po kroku)

### Narzędzia
- **GitHub Desktop** — fork, branch, commit, push (bez terminala do gita)
- **Mousepad** (lub inny prosty edytor tekstu) — wklejanie tłumaczenia do pliku
- **Terminal** — tylko do `cp` (kopiowanie pliku źródłowego) i ewentualnych sprawdzeń `grep`/`curl`

### Etap przygotowania (raz na projekt)
1. Fork repozytorium źródłowego na GitHub (przycisk **Fork**)
2. Sklonować fork lokalnie: GitHub Desktop → **File → Clone repository**
3. Przy pierwszym pushu zaznaczyć **"To contribute to the parent project"** (jeśli celem jest PR do upstreamu) — dzięki temu nowe branche bazują na aktualnym stanie oryginału, a nie na starej kopii forka
4. Sprawdzić `CONTRIBUTING.md` repozytorium źródłowego — może zawierać wymagania specyficzne dla tłumaczeń (np. z którego brancha/taga korzystać, jak nazwać katalog językowy, czy jest szablon Issue)
5. Utworzyć **jeden branch zbiorczy** dla całego tłumaczenia, np. `pl/<nazwa-projektu>-translation` — wszystkie pliki trafiają do tego samego brancha, bo docelowo to będzie jeden PR

### Cykl pracy nad każdym plikiem
1. **Pobranie oryginału** — Claude pobiera treść pliku źródłowego (np. przez `curl`/`web_fetch`), weryfikując dokładną nazwę pliku, jeśli nie jest pewna (numeracja plików bywa nieoczywista — np. w ASVS był skok z `0x05` do `0x10`)
2. **Tłumaczenie do recenzji** — Claude prezentuje pełny tekst tłumaczenia w jednym czystym bloku do skopiowania (bez instrukcji do ręcznego wycinania) + listę NOWYCH decyzji terminologicznych do zatwierdzenia. Długie rozdziały (>1500 słów) dzielone na 2–3 części recenzyjne, ale finalnie sklejane w jeden blok do wklejenia
3. **Akceptacja** — użytkownik potwierdza słowem-kluczem (patrz sekcja "Skróty konwersacyjne" niżej) lub zgłasza poprawki
4. **Kopiowanie pliku źródłowego:**
   ```bash
   cp <repo>/<ścieżka>/en/<nazwa-pliku> <repo>/<ścieżka>/<kod-języka>/<nazwa-pliku>
   ```
   (nazwa pliku identyczna jak w oryginale — tylko katalog się zmienia; kopiowanie zamiast tworzenia pustego pliku gwarantuje 100% zgodność struktury)
5. **Wklejenie tłumaczenia:**
   ```bash
   mousepad <repo>/<ścieżka>/<kod-języka>/<nazwa-pliku>
   ```
   Ctrl+A → wklej zaakceptowany blok → Ctrl+S → zamknij
6. **Commit** w GitHub Desktop:
   - Summary: `Add Polish translation of <nazwa-pliku-bez-rozszerzenia>` (tryb rozkazujący, po angielsku, konkretnie)
   - Description: puste (chyba że trzeba wyjaśnić "dlaczego")
   - **Push origin** od razu po commicie
7. **Przed każdym commitem** — rzucić okiem na listę plików w zakładce **Changes**; commitować tylko to, co świadomie zmieniono (unikać przypadkowych plików-śmieci)

### Higiena i QA
- **Nigdy nie pracować bezpośrednio na `master`** — zawsze na dedykowanym branchu
- Po zakończeniu całości: **fetch + merge upstream** (Branch → Merge into current branch → wybrać `master`), żeby branch tłumaczenia był zsynchronizowany z najnowszym stanem oryginału przed PR
- **Skan spójności terminologii** przed PR — grep po kluczowych terminach i wariantach (np. czy nigdzie nie wkradł się inny przekład tego samego pojęcia), sprawdzenie niedomkniętych nawiasów `[...]` w linkach Markdown, podwójnych spacji jako sygnału przypadkowych literówek
- **Porównanie brancha z aktualnym stanem repo źródłowego** (branch vs. branch/tag wskazany w CONTRIBUTING.md) — jeśli się różnią, sprawdzić czy to realna rozbieżność merytoryczna czy tylko drobne poprawki

### Przed PR
1. **Nigdy nie otwierać PR bez wcześniejszego Issue** (ogólna zasada w projektach OWASP i dobra praktyka open source w ogóle)
2. Issue: krótkie, rzeczowe, po angielsku — co przetłumaczono, link do brancha, pytania do maintainerów (np. który branch/tag ma być bazą, czy jeden PR czy kilka mniejszych)
3. Czekać na odpowiedź maintainerów — w małych, wolontariackich projektach reakcja może zająć tygodnie/miesiące; to normalne
4. Dopiero po zielonym świetle: **Compare & pull request**

### Skróty konwersacyjne (ustalone z Piotrem)
- **"g"** = "gotowe" — krok wykonany, przejdź dalej
- **"s"** = "super" — treść tłumaczenia i decyzje terminologiczne zaakceptowane, przejdź do kroków technicznych

### Kluczowa zasada UX rozmowy
- **Jeden mały krok na wiadomość** — nie łączyć wielu działań technicznych w jednym poleceniu, nawet jeśli się powtarzają
- Każdy krok tłumaczony z **wyjaśnieniem "dlaczego"** (budowanie realnej kompetencji w git/GitHub, nie tylko wykonywanie poleceń)
- Finalna treść do wklejenia zawsze jako **jeden czysty blok kopiuj-wklej** — bez fragmentów wymagających ręcznego okrawania

---

## 3. Zasady stylu tłumaczenia

- **Rejestr:** formalny, profesjonalny, pełne zdania, bez potocznych skrótów myślowych
- **Wzorzec wymagań/instrukcji weryfikacyjnych:** "Verify that..." → **"Zweryfikuj, że..."** — konsekwentnie w każdym wystąpieniu
- **Pierwsze wystąpienie terminu technicznego/skrótu:** polskie tłumaczenie + oryginał w nawiasie (albo odwrotnie — który szyk czyta się naturalniej); dalej: sama ustalona forma
- **Nazwy klas ataków, podatności, protokołów, wzorców projektowych** (np. SSRF, XXE, CSRF, PKCE, DPoP, circuit breaker, race condition) — **zasadniczo bez tłumaczenia**, ewentualnie z polskim opisem w nawiasie przy pierwszym użyciu
- **Tytuły RFC, nazw własnych dokumentów, Cheat Sheet Series** — bez tłumaczenia (to nazwy własne); zwykłe opisowe teksty linków (nie tytuły) — tłumaczone
- **Linki:** tłumaczony tylko tekst kotwicy, **URL nigdy nie modyfikowany**
- **Cudzysłów:** polski „..." zamiast prostego "..."
- **Liczby:** polska notacja (spacja jako separator tysięcy: `210 000`, nie `210,000`)
- **Język normatywny RFC 2119** (MUST/SHOULD/MAY) → **MUSI/POWINIEN/MOŻE** wielkimi literami, zachowując siłę normatywną oryginału
- **Noty prawne, copyright, licencje** — zwyczajowo bez tłumaczenia
- **Nazwiska w tekście ciągłym** — odmieniane po polsku; **w tabelach** — bez zmian
- **Formatowanie Markdown** (nagłówki, tabele, listy, bloki kodu, komentarze HTML typu `<!-- ... -->`) — **zachowywane 1:1** z oryginałem
- **Nazwa pliku tłumaczenia** — identyczna jak w źródle, jedyna zmiana to katalog (np. `en/` → `pl/`)
- Struktura dużych dokumentów referencyjnych (np. glosariuszy) — zachować oryginalny porządek/alfabet **angielskich haseł głównych**, żeby ułatwić przyszłe porównania (diff) z oryginałem i wyszukiwanie po skrótach

---

## 4. Glosariusz terminologiczny (EN → PL)

*Alfabetycznie wg angielskiego terminu. Terminy oznaczone "—" pozostają bez tłumaczenia (nazwy własne, protokoły, klasy ataków, żargon branżowy).*

| Angielski | Polski | Uwagi |
|---|---|---|
| access token | token dostępu | |
| account lockout | blokowanie kont | |
| adaptive response | odpowiedź adaptacyjna | |
| adversary-in-the-middle | — | celowo nie "man-in-the-middle" |
| allowlist | lista dozwolonych | nie "biała lista"/"whitelist" |
| architectural spikes | — (z "tzw.") | żargon agile |
| assertion (SAML/JWT) | asercja | |
| assurance | poświadczenie | usługi/działania poświadczające |
| atomic operation | operacja atomowa | |
| attack surface | powierzchnia ataku | |
| audience (aud) | odbiorca (audience) | |
| audit trails | ślady audytowe | |
| authenticated encryption | szyfrowanie uwierzytelnione | |
| authorization flow | przepływ autoryzacji | |
| authorization server (AS) | serwer autoryzacji (AS) | |
| back-channel logout | wylogowanie kanałem zwrotnym (back-channel logout) | |
| back-off algorithms | — | nie "algorytmy wycofania" |
| backchannel | kanał zwrotny (backchannel) | |
| backdoor | — | |
| backend-for-frontend | — | nazwa wzorca |
| black box testing | testowanie „czarnoskrzynkowe" | |
| BOLA / BOPLA / IDOR | — | nazwy klas podatności OWASP API |
| breached passwords | hasła ujawnione w wyciekach | |
| brute forcing (hasła) | ataki siłowe / łamanie metodą siłową | |
| buffer overflow | przepełnienie bufora | |
| build | — | żargon |
| build pipeline | potok budowania | |
| by exception (raportowanie) | „przez wyjątek" | żargon audytowy |
| chained (vulnerabilities) | łączone w łańcuchy | |
| challenge nonce | wyzwanie (challenge nonce / nonce) | |
| cheat sheet | „ściąga" (potocznie) | "Cheat Sheet Series" jako nazwa projektu bez zmian |
| cipher suites | zestawy szyfrów (cipher suites) | |
| circuit breaker | — | nazwa wzorca |
| claims (JWT/OIDC) | oświadczenia | |
| code flow | przepływ kodu (code flow) | |
| collision resistant | odporne na kolizje | |
| concurrent sessions | sesje równoczesne (równoległe) | |
| confidential client | klient poufny | |
| configuration drift | dryf konfiguracji | |
| connection pool | pula połączeń | |
| consent / consent management | zgoda / zarządzanie zgodami | |
| constant-time | w czasie stałym | |
| consume (o tokenach) | konsumować | |
| consumer | konsument | szeroki termin: user/server/client |
| content sniffing | sniffing treści | |
| credential rotation | rotacja poświadczeń | |
| credential stuffing | — | |
| credentials | poświadczenia | |
| cross-JWT confusion | pomylenie różnych JWT (cross-JWT confusion) | |
| crypto agility | zwinność kryptograficzna (crypto agility) | |
| cryptographic inventory | inwentarz kryptograficzny | |
| cryptographic primitives | prymitywy kryptograficzne | |
| dangerous functionality | „niebezpieczna funkcjonalność" | zdefiniowany termin, w cudzysłowie |
| dangling pointers | wiszące wskaźniki | |
| data exfiltration | eksfiltracja danych | |
| data in use / in transit | dane w użyciu / w tranzycie | |
| deadlocks | zakleszczenia | |
| defense in depth | obrona w głąb | |
| denial of service (DoS) | odmowa usługi | skrót DoS bez zmian |
| dependency confusion | — | |
| device security posture | stan bezpieczeństwa urządzenia | odróżnić od "poziomu bezpieczeństwa" (org.) |
| dictionary attacks | ataki słownikowe | |
| directory listing | listowanie katalogów | |
| disk encryption | szyfrowanie dysków | |
| domain parameters | parametry dziedziny | |
| eavesdropping | podsłuch | |
| economy of design | ekonomia projektowania | |
| elevation of privilege | eskalacja uprawnień | |
| encrypt-then-MAC | — | nazwa trybu |
| endpoint | — | nie "punkt końcowy" |
| entitlements | uprawnienia | |
| escaping | escapowanie | |
| Fermat factorization | faktoryzacja Fermata | |
| field-level/function-level access | dostęp na poziomie pól/funkcji | |
| Finite Field (kryptografia) | ciało skończone | |
| first-party applications | aplikacje własne (first-party) | |
| flood attacks | ataki zalewowe (flood) | |
| forward secrecy | utajnianie z wyprzedzeniem (forward secrecy) | |
| Frontispiece | Strona tytułowa | |
| gateway servers | serwery bramek | |
| GDPR | RODO | oficjalna polska nazwa |
| graceful degradation | kontrolowana degradacja (graceful degradation) | |
| grant (OAuth) | — | nie "przyznanie" |
| hardened | utwardzone | |
| hash (czasownik) | haszować | |
| hash function | funkcja skrótu | |
| header field | pole nagłówka | |
| header injection | wstrzyknięcie nagłówków | |
| high-assurance | o wysokim poziomie pewności | |
| high-signal data | dane o wysokiej wartości sygnałowej | |
| HSM (Hardware Security Module) | sprzętowy moduł bezpieczeństwa | skrót bez zmian |
| hybrid penetration testing | testy penetracyjne hybrydowe | |
| identity proofing | potwierdzenie tożsamości | |
| Identity Provider (IdP) | dostawca tożsamości (IdP) | |
| immutable infrastructure | infrastruktura niezmienna (immutable) | |
| inactivity timeout | limit czasu bezczynności | |
| initialization vectors | wektory inicjujące | |
| integer overflow | przepełnienie liczb całkowitych | |
| Integer Factorization (kryptografia) | faktoryzacja liczb całkowitych | |
| intermediary layer | warstwa pośrednicząca | |
| introspection | introspekcja | |
| key agreement | uzgadnianie klucza | |
| key confusion | — (z opisem PL w nawiasie) | |
| key material | materiał klucza | |
| key stretching | rozciąganie klucza (key stretching) | |
| key vault | skarbiec kluczy (key vault) | |
| key wrapping | opakowywanie kluczy (key wrap) | wrap key → klucz opakowujący |
| LFI / RFI | — | nazwy klas ataków |
| livelocks | uwięzienia | |
| load balancer | moduł równoważenia obciążenia | |
| log injection | wstrzyknięcie do logów (log injection) | |
| lookup secrets | sekrety odszukiwane (lookup secrets) | |
| MAC (Message Authentication Code) | kod MAC | |
| MAC tag | znacznik MAC | |
| magic bytes | „magiczne bajty" | |
| Major.Minor.Patch | — (z rozwinięciem PL w nawiasie) | |
| malformed packets | zniekształcone pakiety | |
| masked (dane) | maskowane | |
| mass assignment | — | nazwa podatności |
| Memorized Secrets (NIST) | „zapamiętane sekrety" (Memorized Secrets) | |
| message body | treść komunikatu | |
| middleware | oprogramowanie pośredniczące | |
| mitigating controls | mechanizmy kompensujące | |
| mix-up attacks | ataki mix-up | |
| multi-factor authentication (MFA) | uwierzytelnianie wieloskładnikowe | skrót MFA bez zmian |
| multi-tenant | wielodostępny | tenant → najemca |
| off the shelf tool | gotowe narzędzie z półki | |
| origin (ogólnie) | źródło | nazwy polityk (Same Origin Policy) bez zmian |
| out-of-band | pozapasmowy (out-of-band) | |
| Padding Oracle | — | nazwa ataku |
| padding schemes | schematy dopełnienia | |
| passkeys | — | nazwa technologii FIDO |
| passphrase | fraza hasłowa | |
| password brute force | łamanie haseł metodą siłową | |
| password strength meter | miernik siły hasła | |
| path traversal | — | |
| peers (WebRTC) | uczestnicy | |
| Principle of Least Privilege (POLP) | zasada najmniejszych uprawnień (POLP) | |
| privacy-enhancing technologies | technologie wzmacniające prywatność | |
| procurement | zakup | |
| Proof-of-Possession, DPoP, PKCE, PAR, JAR, mTLS | — | nazwy mechanizmów OAuth |
| prototype pollution | — | nazwa podatności |
| public client | klient publiczny | |
| purged (dane) | usuwane | |
| push bombing | — | |
| quota | przydział | |
| race conditions | wyścigi (race conditions) | |
| rate limiting | ograniczanie częstotliwości żądań | |
| red flag | sygnał ostrzegawczy | |
| redirect URI | URI przekierowania | |
| reference tokens | tokeny referencyjne | |
| Relying Party (RP) | strona ufająca (Relying Party, RP) | |
| replay attacks | ataki powtórzeniowe | |
| request smuggling | — | |
| resource-demanding | zasobożerny | |
| resource owner (RO) | właściciel zasobu (RO) | |
| resource server (RS) | serwer zasobów (RS) | |
| response splitting | — | |
| retention | retencja | |
| revoke (token) | odwołać | odróżnić od "unieważnić" (invalidate) |
| risky components | „komponenty ryzykowne" | zdefiniowany termin, w cudzysłowie |
| salami attacks / logic bombs / time bombs | ataki salami / bomby logiczne / bomby czasowe | |
| salt | sól | |
| sanitize / sanitization | sanityzować / sanityzacja | |
| SBOM (Software Bill of Materials) | — | |
| schema validation | walidacja schematem | |
| secret questions | „pytania bezpieczeństwa" | |
| secure baseline | bezpieczna linia bazowa | |
| security posture | poziom bezpieczeństwa | (alternatywa: "postawa bezpieczeństwa") |
| seed / seeding | ziarno / zasilanie generatora (seeding) | |
| self-contained tokens | tokeny samowystarczalne | |
| self-signed certificates | certyfikaty samopodpisane | |
| sender-constrained tokens | tokeny ograniczone do nadawcy (sender-constrained) | |
| service accounts | konta usługowe | |
| service mesh | — | |
| signaling / signaling server | sygnalizacja / serwer sygnalizacyjny | |
| single-factor authentication | uwierzytelnianie jednoskładnikowe | |
| single sign-on (SSO) | jednokrotne logowanie | |
| sliding expiration | przesuwne wygasanie | |
| smart cards | karty inteligentne | |
| social engineering | socjotechnika | |
| soft token / hardware token | token programowy / token sprzętowy | |
| something you know | „coś, co wiesz" | triada uwierzytelniania |
| spoofing / tampering (STRIDE) | — (z opisem PL w nawiasie) | |
| SQL/LDAP/XPath/LaTeX injection itp. | wstrzyknięcie SQL/LDAP/XPath/LaTeX | rodzina "wstrzyknięć" |
| SSRF | — | |
| stack traces | ślady stosu | |
| stateful / stateless | stanowy / bezstanowy | |
| step-up authentication | uwierzytelnianie stopniowe | |
| storage exhaustion | wyczerpanie przestrzeni dyskowej | |
| symlinks | dowiązania symboliczne | |
| tampering (ogólnie) | manipulacja | |
| tenant | najemca | |
| the Fallacy of Testability | Złudzenie testowalności | |
| threat modeling | modelowanie zagrożeń | |
| thread-safe | bezpieczny wątkowo | |
| thread starvation | zagłodzenie wątków | |
| throwaway identities | tożsamości jednorazowe | |
| tick marks | symbole zaznaczenia | |
| TLS handshake | uzgadnianie TLS | |
| TOCTOU (time-of-check to time-of-use) | — | |
| token issuer | wystawca tokena | |
| TOTP (Time-based One-Time Password) | hasła jednorazowe oparte na czasie (TOTP) | |
| trackers (użytkowników) | trackery użytkowników | |
| transitive dependencies | zależności przechodnie | |
| trust mark | znak zaufania | |
| trusted service layer | zaufana warstwa usługowa | |
| type juggling / type confusion | — | nazwy podatności |
| UI redress attacks | ataki podmiany interfejsu użytkownika | |
| unmanaged code | kod niezarządzany | |
| untrusted data/input | niezaufane dane (wejściowe) | |
| use-after-free | — | |
| user agent | agent użytkownika | |
| user stories | historyjki użytkownika | |
| user trackers | trackery użytkowników | |
| Verify that... | **Zweryfikuj, że...** | kluczowy wzorzec — każde wymaganie |
| Web Cache Deception | — | |
| web fonts | fonty webowe | |
| WebSocket handshake | uzgadnianie WebSocket | |
| wildcard certificates | certyfikaty typu wildcard | |
| wrap key | klucz opakowujący | |
| XSS / XXE / XSSI / CSRF | — | nazwy klas ataków |
| zip slip | — | |

---

## 5. Skróty i akronimy pozostawiane bez tłumaczenia

`API, SDK, JWT, SAML, OAuth, OIDC, TLS, DTLS, SSL, HTTP(S), URL, URI, UUID, CSPRNG, HSM, TEE, TPM, PKI, CA, WAF, DAST, SAST, SCA, SIEM, SBOM, CI/CD, CVE, CWE, RFC, NIST, FIPS, ISO/IEC, AES, RSA, ECC, ECDH, ECDSA, HMAC, KDF, MAC, GCM, CBC, ECB, PBKDF2, argon2id, scrypt, bcrypt, SRTP, RTP, SDP, STUN, TURN, WebRTC, GraphQL, JSON, XML, CSV, SVG, DOM, CORS, CSP, HSTS, MFA, TOTP, PKCE, DPoP, PAR, JAR, mTLS`

---

## 6. Kontekst projektu (dla wglądu, nieobowiązkowe do wklejenia)

Ten glosariusz powstał przy tłumaczeniu **OWASP ASVS 5.0** (Application Security Verification Standard) na język polski — kompletnym, 27 plików: 5 rozdziałów wstępnych, 17 rozdziałów wymagań (V1–V17), 5 załączników (A–E). Tłumaczenie trafiło do forka `PiotrKleszcz/OWASP-ASVS-Polish-Translation`, branch `pl/asvs-5.0-translation`, zgłoszone jako Issue #3386 w `OWASP/ASVS` przed otwarciem PR.

Styl wzorowany na wcześniejszym tłumaczeniu **OWASP Top 10 for LLM Applications** tego samego autora (`OWASP-LLM-Top10-Polish-Translation`).
