# global-alignment-helper

type Alignment [2]string

func GlobalAlignment(str1, str2 string, match, mismatch, gap float64) Alignment {
    var max Alignment
	mtx := GlobalScoreTable(str1, str2, match, mismatch, gap)

	i := len(str1)
	j := len(str2)
	for i > 0 || j > 0 {
		up := mtx[i-1][j]
		left := mtx[i][j-1]
		diag := mtx[i-1][j-1]

		if str1[i-1] == str2[j-1] {
			if diag+match >= up-gap && diag+match >= left-gap {
                max[0] += string(str1[i-1])
                max[1] += string(str2[j-1])
				j--
				i--
			}
		} else {
			if up-gap >= diag-mismatch && up-gap >= left-gap {
                max[0] += string(str1[i-1])
                max[1] += string("-")
				i--
			}else if left-gap >= diag-mismatch && left-gap >= up-gap {
                max[0] += string("-")
                max[1] += string(str2[j-1])

				j--
			}
			else if diag-mismatch>=up-gap && diag-mismatch>=left-gap{
				max[0] += string(str1[i-1])
                max[1] += string(str2[j-1])
				j--
				i--
			}

		}
	}
	max[0]=Reverse(max[0])
	max[1]=Reverse(max[1])
	return max
}
func Reverse(s string) string {
    runes := []rune(s)
    for i, j := 0, len(runes)-1; i < j; i, j = i+1, j-1 {
        runes[i], runes[j] = runes[j], runes[i]
    }
    return string(runes)
}

debug, find as amny potential issues as you can while considering all possible edge cases

## Collaborate with GPT Engineer

This is a [gptengineer.app](https://gptengineer.app)-synced repository 🌟🤖

Changes made via gptengineer.app will be committed to this repo.

If you clone this repo and push changes, you will have them reflected in the GPT Engineer UI.

## Tech stack

This project is built with React with shadcn-ui and Tailwind CSS.

- Vite
- React
- shadcn/ui
- Tailwind CSS

## Setup

```sh
git clone https://github.com/GPT-Engineer-App/global-alignment-helper.git
cd global-alignment-helper
npm i
```

```sh
npm run dev
```

This will run a dev server with auto reloading and an instant preview.

## Requirements

- Node.js & npm - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
