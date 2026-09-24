# Decentralizált felülvizsgálat integrációs terv

Ez a terv felülírja a korábbi egyközpontú „controller → végrehajtó” mintát
azoknál a folyamatoknál, amelyek felhasználói adatot, hozzáférést, pénzügyi
jutalmat vagy jogi hatású jelentést érintenek.

## Kötelező adapterek

1. **Signal adapter** – a Carl Edge és a GenesisLLMGuard csak technikai jelet,
   bizonyíték-digestet és kockázati kategóriát ad át.
2. **Review adapter** – legalább három független ellenőri csoport, kötelező
   összeférhetetlenségi nyilatkozat és pseudonymous reviewer-azonosító.
3. **User adapter** – a felhasználó vagy kijelölt képviselő kötelező szavazata,
   kifogás- és fellebbezési csatornája.
4. **Legal adapter** – joghatóság és jogi hatás esetén illetékes emberi
   felülvizsgálat; az agent nem dönthet bűnösségről és nem továbbíthat vakon
   hatósági adatot.
5. **Anchor adapter** – csak hash és minimális állapot kerülhet blokkláncra;
   az encrypted evidence bundle a felhasználó által kezelt vaultban marad.

## Agent-jogosultságok

Az agent tervezhet, összegezhet és hiányzó bizonyítékot jelezhet. Nem adhat
önállóan tartós tiltást, kreditjutalmat, jogi minősítést, személyazonosítást
vagy kulcsfeloldást. Minden külső művelet capability-scoped, lejáró és
visszavonható.
