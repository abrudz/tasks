# Day 11 Summary Notes and Useful Links

## Notes
- Nested arrays: http://course.dyalog.com/autumn2021/Array-model/#nested-arrays
- Assignment: http://course.dyalog.com/autumn2021/Assignment/
- Strand assignment: http://course.dyalog.com/autumn2021/Assignment/#strand-assignment
- Native files: http://course.dyalog.com/autumn2021/Data/#n
- Basic error trapping: http://course.dyalog.com/autumn2021/Errors/#gotta-trap-em-all
- Do NOT rely on errors for behaviour: http://course.dyalog.com/autumn2021/Errors/#who-needs-to-know

## New things:

- Format: `⍕`
- Execute: `⍎`
- Pick: `⊃`
- Enlist: `∊`
- Index function (squished quad: squad): `⌷`
- Mix: `↑`

- Migration level: `⎕ML`
- Data representation: `⎕DR`
- Get text data: `⎕NGET`

## Uneven depth
```
      ≡ 3 (4 5)
¯2
      ≡¨ 3 (4 5)
0 1
      ]display 3 (4 5)
┌→────────┐
│   ┌→──┐ │
│ 3 │4 5│ │
│   └~──┘ │
└∊────────┘

      ≡ (,3) (4 5)
2
      ≡¨ (,3) (4 5)
1 1
      ]display (,3) (4 5)
┌→──────────┐
│ ┌→┐ ┌→──┐ │
│ │3│ │4 5│ │
│ └~┘ └~──┘ │
└∊──────────┘

      ≡ (⊂,3) (4 5)
¯3
      ≡¨ (⊂,3) (4 5)
2 1
      ]display (⊂,3) (4 5)
┌→──────────────┐
│ ┌─────┐ ┌→──┐ │
│ │ ┌→┐ │ │4 5│ │
│ │ │3│ │ └~──┘ │
│ │ └~┘ │       │
│ └∊────┘       │
└∊──────────────┘
```

## Mix
```
      (3 7⍴'Adam   RodrigoRich   ') ≡ ↑'Adam' 'Rodrigo' 'Rich'
1

      ⍴⍴↑'this' 'that'
2


      ⍴⍴(↑'a' 'b')
1
      'a' 'b' ≡ 'ab'
1
```

## Partitioning
```
⍝ Partitions start at 1 and continue until the next 1
      ]disp 0 0 1 0 1 0 0 0 0⊂'partition'
┌→─┬─────┐
│rt│ition│
└─→┴────→┘

⍝ With migration level 3, partitions begin at increases of ⍺, and 0 omits elements.
      Part←{⎕ML←3 ⋄ ⍺⊂⍵}
      ]disp 1 1 2 2 3 Part 'hello'
┌→─┬──┬─┐
│he│ll│o│
└─→┴─→┴→┘
      ]disp 1 2 0 1 0 5 Part 'apples'
┌→┬─┬─┬─┐
│a│p│l│s│
└→┴→┴→┴→┘
```

## Enclose with axis
```
      ⊂[2]2 3 4⍴⎕A     ⍝ Enclose a single axis
┌───┬───┬───┬───┐
│AEI│BFJ│CGK│DHL│
├───┼───┼───┼───┤
│MQU│NRV│OSW│PTX│
└───┴───┴───┴───┘

      ⊂[3 1]2 3 4⍴⎕A   ⍝ Enclose multiple axes (can re-order)
┌──┬──┬──┐
│AM│EQ│IU│
│BN│FR│JV│
│CO│GS│KW│
│DP│HT│LX│
└──┴──┴──┘
```
