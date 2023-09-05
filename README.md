# container-validator

Demo link: https://container-validator.vercel.app/

<img width="680" alt="container1" src="https://github.com/jafar-maersk/container-validator/assets/88651509/d6eb7706-1216-4559-898d-c8de02a18ce0">

Cargo container validator ISO 6346

Install
=======

```html
<script type="text/javascript" src="ContainerValidator.js"></script>
```
 
Install using Bower:
====================

bower install Container-validator-JS


Documentation
=============

Validate container ISO codes (TEXU3070079 = valid, TEXU3070070 != valid)

```javascript
validator = new ContainerValidator();
validator.isValid('TEXU3070079'); // boolean true
validator.isValid('TEXU3070070'); // boolean false
```

To get the diffrent segments from the code you can do,

```javascript
container = validator.validate('TEXU3070079');
console.log(container); // Array ( [0] => TEXU3070079 [1] => TEX [2] => U [3] => 307007 [4] => 9 )
```
where:

```javascript
array
  0 => string 'TEXU3070079' // The code being validated
  1 => string 'TEX' // The containers ownercode
  2 => string 'U' // The containers group code
  3 => string '307007' // The containers registration digit
  4 => string '9' // The containers check digit
```

How to get error messages when the container code is invalid

```javascript
validator.validate('TEXU3070070');
validator.getErrorMessages(); // The check digit does not match

validator.validate(12345678910);
validator.getErrorMessages(); // The container number must be a string

validator.validate('C3P0');
validator.getErrorMessages(); // The container number is invalid
```

Access information about the container:
```javascript
validator.validate('TEXU3070070');
console.log(validator.getOwnerCode()); // TEX
console.log(validator.getProductGroupCode()); // U
console.log(validator.getRegistrationDigit()); // 307007
console.log(validator.getCheckDigit()); // 9
```

Create a check digit to a container that does not have one
```javascript
validator = new ContainerValidator();
validator.createCheckDigit('TEXU307007'); // 9
```

Generate container numbers:
```javascript
// validator.generate( owner-code, product-group-code, number-start, number-end );
validator = new ContainerValidator();
validator.generate('TEX','U',1, 100 ));


Owner code
The owner code consists of three capital letters of the Latin alphabet to indicate the owner or principal operator of the container. Such code needs to be registered at the Bureau International des Containers in Paris to ensure uniqueness worldwide. An owner can apply for more than one code, as normally the first 2 letters are used as the owner code and the third is used to indicate pool (e.g. HLA, HLB, HLX are some Hapag-Lloyd codes to indicate whether container is standard, reefer...)

Equipment category identifier
The equipment category identifier consists of one of the following capital letters of the Latin alphabet:

U for all freight containers
J for detachable freight container-related equipment
Z for trailers and chassis
Presently, all official BIC container codes end in "U". However, the Association of American Railroads recognizes similar codes for their containers and trailers travelling by rail in North America, though these are not recognized by the BIC and lack check digits.

Under the ISO code, then, only U, J, and Z are in use. The refrigerated (reefer) container is identified by means of the size type code.

Serial number
The serial number consists of 6 numeric digits, assigned by the owner or operator, uniquely identifying the container within that owner/operator's fleet.

Check digit
The check digit consists of one numeric digit providing a means of validating the recording and transmission accuracy of the owner code and serial number.
