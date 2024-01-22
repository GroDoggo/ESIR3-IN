*AV1 Bitstream and decoding process specification*
## Lexique
- **Altref** -> Alternative reference frame
- **Base layer** -> Layer with spatial and temporal id 0
- **Bitstream** -> sequence of bytes created by the encoding of the video
- **Byte alignment** -> One bit is byte aligned if the position of the bit is an integer multiple of eight from the position of the first bit in the bitstream
- **CDEF** -> Filter block based on identify a direction
- **CDF** -> Probability times 32768 that a symbol has value less than or equal to a level

### Opérations bitstream
```c#
uint x = 0b_1001;
Console.WriteLine($"Before: {Convert.ToString(x, toBase: 2), 4}");

uint y = x >> 2;
Console.WriteLine($"After:  {Convert.ToString(y, toBase: 2).PadLeft(4, '0'), 4}");
// Output:
// Before: 1001
// After:  0010
```
### Descriptors
#### F(n)
Lit les n prochains bit et en retourne un nombre
```c++
x = 0
for ( i = 0; i < n; i++ ) {
x = 2 * x + read_bit( )
}
//BITSTREAM : 011...
//INPUT : f(3)
/* Boucle 1 : x = 2 * 0 + 0 = 0
Boucle 2 : x = 2 * 0 + 1 = 1
Boucle 3 : x = 2 * 1 + 1 = 3
Resultat : x = 3 (011 en binaire) */
```
**Remarque** : le MSB est lu en premier
#### UVLC()
Lit un nombre entier non-signé de taille variable
```c++
uvlc() {
	leadingZeros = 0
	while ( 1 ) {
		done = f(1)
		if ( done )
			break
		leadingZeros++
	}
	if ( leadingZeros >= 32 ) {
		return ( 1 << 32 ) - 1
	}
	value = f(leadingZeros)
	return value + ( 1 << leadingZeros ) - 1
}
```
