# Angular Noter

## Indhold
[Next()](#next)  
[onDestroy](#ondestroy)  

## onDestroy

nDestroy er en Angular lifecycle hook — altså en metode, du kan implementere i din komponentklasse, som Angular automatisk kalder lige før komponenten bliver fjernet (dvs. destroyed) fra DOM'en.

### Hvad gør OnDestroy?
Det er en måde at rydde op på, når komponenten lukkes eller navigeres væk fra.

Typisk bruger man ngOnDestroy() til at afmelde (unsubscribe) fra RxJS-observables eller event listeners for at undgå memory leaks (hukommelseslækager).

Hvis du fx har en Subscription fra en Observable, skal du unsubscribe i ngOnDestroy() for at stoppe data-streamen og frigive ressourcer.

### Hvordan bruges det?
Du implementerer OnDestroy-interfacet og skriver en ngOnDestroy() metode:

```typescript
import { Component, OnDestroy } from '@angular/core';
import { Subscription } from 'rxjs';

@Component({...})
export class MyComponent implements OnDestroy {
  private subscription: Subscription;

  constructor() {
    this.subscription = someObservable.subscribe(data => {
      // gør noget med data
    });
  }

  ngOnDestroy() {
    // Når komponenten bliver fjernet, ryd op:
    this.subscription.unsubscribe();
  }
}
```
### Hvorfor er det vigtigt?
Hvis du ikke unsubscribe, kan dit abonnement fortsætte med at køre i baggrunden, selvom komponenten ikke længere vises, hvilket kan føre til:
- Dårlig ydelse
- Hukommelseslækager

---
[Home](#indhold)
## Next()
Metoden next() kommer fra Subject i RxJS (Reactive Extensions for JavaScript), som Angular bruger til at håndtere streams og asynkrone data.

### Hvad betyder next()?
next(value) sender en ny værdi (her: query) ud til alle, der abonnerer (subscribes) på denne Subject.

Altså: Når du kalder this.searchQuerySubject.next(query), fortæller du alle, der lytter på searchQuerySubject, at der er kommet et nyt søgeord.

De komponenter eller services, som har lavet subscribe() på searchQuerySubject.asObservable(), modtager denne nye værdi og kan reagere på den (f.eks. hente nye data fra API).

### En analogi:
Forestil dig et radio broadcast:

searchQuerySubject er radiokanalen.

next(query) er som at sende en ny besked ud på kanalen.

Alle, som har tændt radioen (subscribet), hører beskeden med det samme.

### Opsummering:
next() = send ny værdi til alle abonnenter.

I dit tilfælde: Når brugeren skriver noget i søgefeltet og trykker søg, sender du søgeordet ud, og LandingpageComponent modtager det og kan opdatere listen af bøger.
