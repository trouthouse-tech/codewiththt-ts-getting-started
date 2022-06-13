Hola hola,

Using TypeScript in your React Native (RN) projects can seem like a daunting task - and it definitely can be. I would recommend experimenting/practicing in a fresh RN project before updating your production app to TypeScript.

#### Getting Started

[Here](https://github.com/trouthouse-tech/codewiththt-ts-getting-started) is a fresh repo created using the the command found [here](https://reactnative.dev/docs/typescript#getting-started-with-typescript).

#### JSX
One good thing about this endeavor is that our JSX (the stuff between the `return ()`) won't change much.

#### JavaScript Component (.js)
Let's take a look at a very simple JS component that accepts in a text prop and displays that inside of a simple `<Text>` component.

```
const MyTextComponent = (props) => {
  const {text} = props;

  return (
    <Text>{text}</Text>
  );
}
```

#### TypeScript Component (.tsx)
Here's the same exact component but using TS. You'll notice that not much has changed within the actual component.

```
type Props = {
 text: string;
};

const MyTextComponent = (props: Props) => {
  const {text} = props;

  return (
    <Text>{text}</Text>
  );
}
```
All we're doing differently is saying that the props passed to `MyTextComponent` should contain only one property called `text` and that prop should be a `string`. 

This set of _rules_ will let us know that there is an issue if we try to do the following:

`<MyTextComponent text={5} />`

Will the above crash? No. But, it alert us right away.

#### TypeScript With Local State
Here is how we can update our local state ([useState](https://reactjs.org/docs/hooks-state.html)) to utilize TypeScript.

```
import {TextInput, TouchableOpacity} from 'react-native';

const MyTextInputComponent = () => {
  // const [text, setText] = useState(''); // JS version
  const [text, setText] = useState<string>(''); // TS version

  const incrementText = () => {
    setText(oldVal => oldVal + 1); // TS will yell at us here
  };

  return (
    <>
      <TextInput onChangeText={setText} value={text} />
      <TouchableOpacity onPress={incrementText}>
        <Text>Increment Text</Text>
      </TouchableOpacity>
    </>
  );
}
```
In the above example, we set a type for our local state by using the angle bracket notation to say that this `text` value should only be a `string`. 

<u>_Why would TS yell at us for the `incrementText()` button?_</u>
TS knows that the `text` prop is a `string`. When we write code like `setText(oldVal => oldVal + 1);` which is adding 1 to the old `text` value TS will warn us that we cannot add a `Number` and a `string`. 

#### `.ts` vs `.tsx`
You'll see both of these files. `.ts` files are used for non-UI logic (i.e., stuff not within a `return()` statement). In order to display a UI component (like `<View>, <Text>, and etc` you need to make sure that you are in a `.tsx` file.

#### Summary
- I don't recommend adding TypeScript to a production app if it's your first time
- Your JSX will mostly stay the same
- TypeScript is your friend

Happy coding!

- Matt
