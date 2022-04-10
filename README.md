# CodeCraftSunday-2022-04-10

Used: https://gist.github.com/gregorriegler/5c578410a619188838d3c9c6c23e09ae

Given a letter print a diamond starting with 'A' with the supplied letter at the widest point.

This is the print diamond for 'E'.

....A....
...B.B...
..C...C..
.D.....D.
E.......E
.D.....D.
..C...C..
...B.B...
....A....


This is the print diamond for 'C'.

..A..
.B.B.
C...C
.B.B.
..A..

This is the print diamond for 'A'.

A

Note: These examples use dots in place of spaces only for readability.
Your diamond must contain spaces where there are dots.

---

Retro:

How did that feel?
- Cumbersome +1
- Rewarding +1
- Good, Surprising (Gitpod) +2
- Proud
- More mature (with gitpod)
- Disappointed about whitespace handling in multiline Strings

What worked well, need to do it more?
- Consistent with Rotation
- TDD Bootsrap Script +2
- Using Refactoring tools of VS Code
- Look into Gitpod workspaces
- Split Screen

---

// Code as of 4/10/2022 5:53 PM EDT

import {expect} from 'chai'
import 'mocha'

describe('Diamond', () => {
    it('is the simplest Diamond', () => {
        expect(diamond('A')).to.equal('A')
    })

    it('is the Diamond for B', () => {
        expect(diamond('B')).to.equal(
`.A.
B.B
.A.
`
        )
    })

    it('is the Diamond for C', () => {
        expect(diamond('C')).to.equal(
`..A..
.B.B.
C...C
.B.B.
..A..
`
        )
    })
})

function diamond(letter: string): string {
    if(letter === 'C') {
        const top = "..A.." + "\n";
        return top +
               ".B.B." + "\n" +
               middleLine("C") +
               ".B.B." + "\n" +
               top; 
    }

    if(letter === 'B') {
        let middle = middleLine(letter);
        let top = topLine(letter);
        return top + middle + top;
    }
    return 'A';
}

function topLine(diamondLetter: string) {
    const spacesInMiddle = numberOfSpacesInMiddle(diamondLetter);
    const diamondWidth = spacesInMiddle + 2;
    const spacesInTopSide = (diamondWidth - 1) / 2;
    let dots = '.'.repeat(spacesInTopSide);
    return dots + 'A' + dots + '\n'
}

function middleLine(diamondLetter: string) {
    return diamondLetter + '.'.repeat(numberOfSpacesInMiddle(diamondLetter)) + diamondLetter + '\n'
}

function numberOfSpacesInMiddle(diamondLetter: string) {
    return (diamondLetter.charCodeAt(0) - 'A'.charCodeAt(0)) * 2 - 1;
}
