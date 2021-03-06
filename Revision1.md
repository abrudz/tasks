```
      )clear
clear ws

       1 2 3+10
11 12 13
       1 2 3+10 20 30
11 22 33
       +/10 20 30
60
      2 36
2 36
      2 3⍴⍳6
1 2 3
4 5 6
      +⌿2 3⍴⍳6
5 7 9
      +/2 3⍴⍳6
6 15
      ⍴+/2 3⍴⍳6
2
      ,2 3⍴⍳6
1 2 3 4 5 6
      ⍴2 3⍴⍳6
2 3
      ⍴⍴2 3⍴⍳6
2
      3 4⍴⍳12
1  2  3  4
5  6  7  8
9 10 11 12
      2 2↑3 4⍴⍳12
1 2
5 6
      2 2↓3 4⍴⍳12
11 12
      1 0 1 1/3 4⍴⍳12
1  3  4
5  7  8
9 11 12
      1 0 1⌿3 4⍴⍳12
1  2  3  4
9 10 11 12
        1∧0
0
        1∧1
1
      ∨/1 0 0 1
1
      ∧/1 0 0 1
0
      +/1 0 0 1
2
      +/1 0 0 0 1
2
      +/~1 0 0 0 1
3
      ∧/~1 0 0 0 1
0
      ∨/~1 0 0 0 1
1

nums←3 5⍴⍳12
nums+←5       ⍝ Modified assignment; nums changes value after this expression is executed

⍳¨⍳5    ⍝ Each ¨ is used with nested arrays
∊⍳¨⍳5   ⍝ Enlist ∊ removes nested structure and returns a simple vector
∊'this' 'nested' 'vector'

⍝ Reduction on a nested vector returns a nested scalar:
×/(1 1 2)(3 1 4)(¯1 0 1)
⍝ Use disclose to "unpack" the array from inside:
⊃×/(1 1 2)(3 1 4)(¯1 0 1)

There are many ways to select elements or sub-arrays from arrays:

↑ ↓ [] ⌷ / ⌿ ⊃

To get the "last" element, pick-reverse:

⊃⌽'ABCDE'   ⍝ Get 'E' quick!

Using indexing or compression will return a scalar or collection of scalars. If selecting from a nested array, the result will be enclosed !

      ]disp (2 3⍴'hello' 'world' 2 3 'ok')[2;2]
┌──┐
│ok│
└─→┘
      ]disp ⊃(2 3⍴'hello' 'world' 2 3 'ok')[2;2]
ok
      ]disp (⊂2 2)⊃(2 3⍴'hello' 'world' 2 3 'ok')
ok

There are first- and last-axis versions of some primitives:
/ ⌿ ⌽ ⊖ , ⍪

Some primitives can work with square brackets to work along any specified axis:

+/[2] 2 3 4⍴⍳24   ⍝ Sum along 2nd axis
 'ann'=[1]↑'oranges' 'mangoes' 'bananas'      ⍝ Equality along 1st axis
'mangoes'=[2]↑'oranges' 'mangoes' 'bananas'   ⍝ Equality along 2nd axis

APL uses 3 types of "brackets". They are called:
- Round parentheses ()
	Used to change order of execution: (2 3⍴⍳6) Function 4 3⍴⍳4

- Square brackets []
	Used for indexing and axis specification

- Curly braces {}
	Used for:
	- shy results in tradfns
		{result}←FnName                  ⍝ This is a tradfn header
	- optional left arguments in tradfns
		{optional} FnName not_optional   ⍝ This is a tradfn header

We often use array techniques in order to express program logic:

      B←2 3 8 5 8
      C←45+7×B=8   ⍝ Set C to 52 if B is 8, 45 otherwise

      heights←?50⍴10
      Buckets←{+⌿⍵∘.=⍳10}
      Histogram←{i,' ⎕'[1+⍵∘.≥i←⍳⍴⍵]}

  ⍝ Try: 
      Histogram Buckets Heights

  ⍝ Or, for other values:

    ∇  hist←AnyHist vector;vals;bins       
[1]    vals←∪vector                        
[2]    bins←+/vals∘.=vector                
[3]    hist←vals,' ',' ⎕'[1+bins∘.≥⍳⌈/bins]
    ∇

  ⍝ Try:
      letters ← 'AEIOU'[?50⍴5]
      AnyHist letters

            ]disp 'early' 'daytime' 'late' {⍺[1++⌿8 17∘.<⍵]} 6 10 12 5 20 15
┌→────┬───────┬───────┬─────┬────┬───────┐
│early│daytime│daytime│early│late│daytime│
└────→┴──────→┴──────→┴────→┴───→┴──────→┘
```
