# pyseq-align
Python interface for the [seq-align](https://github.com/noporpoise/seq-align) C library, written by Isaac Turner (@noporpoise).

### Fork by Yaakov Belch:
I expanded `no_start_gap_penalty` and `no_end_gap_penalty` to:
`no_start_gap_penalty`, `no_start_gap_penalty_a`, `no_start_gap_penalty_b`,
`no_end_gap_penalty`,   `no_end_gap_penalty_a`,   `no_end_gap_penalty_b`.

The feature `no_start_gap_penalty_a` seems not to work, but `no_start_gap_penalty_b` works.
The code is 100% symmetric for all these cases, but investigate `seq-align/src/alignment.c`
where the comments say: `// Think carefully about which way round these are`

The algorithm may not be symmetric.

## Installation
```
pip install pyseq-align
```

To install directly from GitHub,
```
git clone https://github.com/Lioscro/pyseq-align.git --recursive
cd pyseq-align
pip install .
```

## Usage
Two alignment algorithms are provided: Needleman-Wunsch and Smith-Waterman.

```python
from pyseq_align import NeedlemanWunsch

nw = NeedlemanWunsch()
al = nw.align('ACGT', 'ACGTC')
print(al.result_a)  # ACGT-
print(al.result_b)  # ACGTC
print(al.score)
```

```python
from pyseq_align import SmithWaterman

sw = SmithWaterman()
als = sw.align('ACGT', 'ACGTC')  # unlike above, this is a list of Alignment's
for al in als:
    print(al.result_a, al.pos_a)  # ACGT, 0
    print(al.result_b, al.pos_b)  # ACGT, 0
    print(al.score)
```
