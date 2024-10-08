# Tic Tac Toe Game

- Installing React Native Vector Icons

```
npm install --save react-native-vector-icons
```

## Android Setup for Vector Icons

To make font management smoother on Android, use this method:

- Edit android/app/build.gradle (NOT android/build.gradle) and add:

```
apply from: file("../../node_modules/react-native-vector-icons/fonts.gradle")
```

## Icons Component Creation

- importing the Icon

```
import Icon from 'react-native-vector-icons/FontAwesome'
```

- it will throw an error which is for libery sucg a FontAwesome that's why we need to install new libery @types/react-native-vector-icons

```
npm i @types/react-native-vector-icons
```

- Created a datatype for that icons

```
type IconsPeop = PropsWithChildren<{
  name: string
}>
```

- Giving a variable of type IconProp and using tha variable as switch case

```
const Icons = ({name}: IconsPeop) => {
   switch (name) {
      case 'circle':
         return <Icon name='circle-thin' size={38} color="#F7CD2E" />
         break;
      case 'cross':
         return <Icon name='times' size={38} color="#38CC77" />
         break;
      default:
         return <Icon name='pencil' size={38} color="#0D0D0D" />
   }
}
```

## App.tsx

- installing Snackbar libery for popups

```
npm i react-native-snackbar
```

- Deciding the state

```
const [isCross, setIsCross] = useState<boolean>(false)
const [gameWinner, setGameWinner] = useState<string>('')
const [gameState, setGameState] = useState(new Array(9).fill('empty', 0, 9))
```

new Array().fill is responsible for filling the space with the value of 'empty' fron 0th index to 9th index

- ReLoad Game:

```
const reloadGame = () => {
    setIsCross(false)
    setGameWinner('')
    setGameState(new Array(9).fill('empty', 0, 9))
}
```

- Chexk Winner for every row and coloum and digonal of the game grid and set Game Winner as decided

```
const checkIsWinner = () => {
   if(
      gameState[0] !== 'empty' &&
      gameState[0] === gameState[1] &&
      gameState[0] === gameState[2]
    ) {
      setGameWinner(`${gameState[0]} Won the Game! 🥳 `)
    } else if (
      gameState[3] !== 'empty' &&
      gameState[3] === gameState[4] &&
      gameState[3] === gameState[5]
    ) {
      setGameWinner(`${gameState[3]} Won the Game! 🥳 `)
    }
}
```

- When Items on the screen changes
  we took Item Number
  if the Game Winner is decided the we pass a snack and set it as gameWinner

```
if(gameWinner){
   return Snackbar.show({
      text: gameWinner,
      backgroundColor: '#d1b008',
      textColor: 'white'
   })
}
```

- If game item Number is empty

```
    if (gameState[itemNumber] === 'empty') {
      gameState[itemNumber] = isCross ? 'cross' : 'circle'
      setIsCross(!isCross)
    } else {
      return Snackbar.show({
        text: 'Provide place is alredy filled',
        backgroundColor: '#e31e1e',
        textColor: 'white'
      })
    }

    // and finally check if the winner is confirm or not
    checkIsWinner()
```
