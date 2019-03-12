# Tests
Following [Willan Justen](https://willianjusten.com.br/) TDD Course here I wil point some usefull informations about it

## Why test?
- Less time spent analysing and correcting bugs
- Easely refactoration
- Documentation
- Better Code design 
- Guarantee quality

## How TDD flow
![TDD flow](https://image.prntscr.com/image/IGyO3DfnRJOV-YtkWYdpXQ.png)

1) Write a code that fails <br>
Write the test, which will fail

2) Make code works <br>
Write the code, simple code (maybe stupid), that the test validates.
 Always a lot of tests for a method, not inverse

3) Refactor

### Test flow
1. Write the test, which obviously will fail
2. Makes the code be validated by test, on a stupid way
3. Write another test for this method
4. Makes the code be validated
5. Write another test, if u want
6. Refactor your code <br>
Garantee your code still valid in a better style

### Think as a Test
1. What the method should do? <br>
All method need to do one thing
2. What data this method will receive?
3. What this method must return?
4. When will this method run?

### Test Pattern
"It should do that when this" <br>
ex.: 
```javascript
it('should return 4 when receive 2,2') {
    expect(sum(2,2)).to.equal(4);
}
```

ex.: `it must add class Active when clicked`