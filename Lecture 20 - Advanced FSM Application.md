# Manchester Encoder/Decoder

Coding scheme widely used in Wired Network Communication for Noise Tolerance.

Filters environment noise from noisy square waves into ideal square digital signals.

## Coding Scheme:
Problems with sending raw digital data due to noise

1. Logic 0: Transition from *LOW* to *HIGH*.
2. Logic 1: Transition from *HIGH* to *LOW*.
* Direction of transition is harder to interfere with than actual voltage levels

### Example:
`0100110100` => `01 10 01 01 10 01 10 01 01`
This is timed with Data Clock ticking at the centre of the NRZ bit. NRZ clock 2x Data Clock

## Decoding:
1. If incoming *HIGH*, expect *HIGH-LOW* transition, output `1`
2. if incoming *LOW*, expect *LOW-HIGH* transition, output `0`
3. After *HIGH-LOW* transition, if *LOW* follows, expect pending *LOW-HIGH* transition, output `1` -> `0`
4. After *LOW-HIGH* transition, if *HIGH* follows, expect pending *HIGH-LOW* transition, output `0` -> `1`
* FSM is triggered at Network Clock Speed

### Example:
