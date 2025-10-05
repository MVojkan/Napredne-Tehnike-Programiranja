# Napredne-Tehnike-Programiranja

# Rad za ocenu 8

# Opis problema: Simulacija dvostrukog klatna (Double Pendulum)

Dvostruko klatno predstavlja fizički sistem koji se sastoji od dva obična (jednostavna) klatna povezana tako da je kraj prvog klatna oslonac drugog.
Sistem čine dve šipke dužina l₁ i l₂, sa masama m₁ i m₂ na krajevima. Prvo klatno je vezano za fiksnu tačku, a drugo za kraj prvog klatna.
Zbog međusobne zavisnosti kretanja, sistem pokazuje nelinearno i haotično ponašanje.

# Osnovna ideja

Za razliku od običnog (jednog) klatna, kod dvostrukog klatna kretanje nije periodično, već vrlo složeno i osetljivo na početne uslove.
To znači da i minimalne razlike u početnim uglovima mogu dovesti do potpuno različitih putanja kroz vreme.
Zbog te osobine, sistem je često korišćen u proučavanju haotičnih dinamičkih sistema.

# Fizički opis

Kretanje sistema se zasniva na zakonima očuvanja energije (potencijalne i kinetičke) i Lagrangeovom formalizmu.
U zavisnosti od položaja oba klatna (θ₁, θ₂), menjaju se ubrzanja i sile, pa se kretanje opisuje sistemom nelinearnih diferencijalnih jednačina drugog reda.
One povezuju uglove, brzine i ubrzanja oba klatna, uzimajući u obzir gravitacionu silu g, mase i dužine šipki.

Matematički model se može zapisati kao:

Dvostruko klatno se opisuje sledećim diferencijalnim jednačinama:

d²θ₁/dt² =
[ -g(2m₁ + m₂) * sin(θ₁)
  - m₂ * g * sin(θ₁ - 2θ₂)
  - 2 * sin(θ₁ - θ₂) * m₂ * (ω₂² * l₂ + ω₁² * l₁ * cos(θ₁ - θ₂))
] /
[ l₁ * (2m₁ + m₂ - m₂ * cos(2θ₁ - 2θ₂)) ]


d²θ₂/dt² =
[ 2 * sin(θ₁ - θ₂) *
  ( ω₁² * l₁ * (m₁ + m₂)
    + g * (m₁ + m₂) * cos(θ₁)
    + ω₂² * l₂ * m₂ * cos(θ₁ - θ₂)
  )
] /
[ l₂ * (2m₁ + m₂ - m₂ * cos(2θ₁ - 2θ₂)) ]


Ove jednačine se ne mogu rešiti analitički, već se koristi numerička aproksimacija — najčešće metod Runge-Kutta 4. reda (RK4) za integraciju u vremenu.


# Računarski aspekt problema

Cilj simulacije je da se proračuna položaj (ugao) svakog klatna u funkciji vremena, na osnovu početnih uslova.
Za svaku vremensku iteraciju, potrebno je:

izračunati ubrzanja prema prethodnim vrednostima uglova i brzina,

ažurirati brzine i položaje,

sačuvati rezultate radi prikaza ili analize.

Pošto se svaka simulacija može izvoditi nezavisno (npr. sa različitim početnim uglovima), problem se lako paralelizuje — svaki proces ili nit može obrađivati jedno klatno ili jednu kombinaciju početnih uslova.
To omogućava poređenje performansi sekvencijalne i paralelne implementacije.

# Cilj projekta

Cilj projekta je da se realizuje:

Sekvencijalna simulacija dvostrukog klatna u Pythonu i Rustu.

Paralelna verzija (više simultanih simulacija) radi merenja performansi.

Rezultat je analiza u kojoj se prikazuje:

razlika u brzini između sekvencijalne i paralelne varijante,

razlika između interpretiranog (Python) i kompajliranog (Rust) pristupa.

