# Angular Noter

# Indhold
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



[Home](#indhold)
