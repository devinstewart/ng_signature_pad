# ng_signature_pad
Angular component for [szimek/signature_pad](https://www.npmjs.com/package/signature_pad).

# Please Note
Initially, this is a fork of [lathonez/angular2-signaturepad](angular2-signaturepad) with the peer depencies updated to allow for Angular 14 - 16 to install without errors.  In future versions, I will address any bugs, issues, or feature requests as the original author has stated he is no longer maintaining future Angular changes.
## Install
`npm install ng_signature_pad --save`

## Usage example

API is identical to [szimek/signature_pad](https://www.npmjs.com/package/signature_pad).

Options are as per [szimek/signature_pad](https://www.npmjs.com/package/signature_pad) with the following additions:
* canvasWidth: width of the canvas (px)
* canvasHeight: height of the canvas (px)
The above options are provided to avoid accessing the DOM directly from your component to adjust the canvas size.

```typescript

// import into app module

import { SignaturePadModule } from 'ng_signature_pad';

...

@NgModule({
  declarations: [ ],
  imports: [ SignaturePadModule ],
  providers: [ ],
  bootstrap: [ AppComponent ]
})

// then import for use in a component

import { Component, ViewChild } from '@angular/core';
import { SignaturePad } from 'ng_signature_pad/signature-pad';

@Component({
  template: '<signature-pad [options]="signaturePadOptions" (onBeginEvent)="drawStart()" (onEndEvent)="drawComplete()"></signature-pad>'
})

export class SignaturePadPage{

  @ViewChild(SignaturePad) signaturePad: SignaturePad;

  signaturePadOptions: Object = { // passed through to szimek/signature_pad constructor
    'minWidth': 5,
    'canvasWidth': 500,
    'canvasHeight': 300
  };

  constructor() {
    // no-op
  }

  ngAfterViewInit() {
    // this.signaturePad is now available
    this.signaturePad.set('minWidth', 5); // set szimek/signature_pad options at runtime
    this.signaturePad.clear(); // invoke functions from szimek/signature_pad API
  }

  drawComplete() {
    // will be notified of szimek/signature_pad's onEnd event
    console.log(this.signaturePad.toDataURL());
  }

  drawStart() {
    // will be notified of szimek/signature_pad's onBegin event
    console.log('begin drawing');
  }
}
```
