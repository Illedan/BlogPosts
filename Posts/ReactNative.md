{"Tags":["Mac", "React", "iOS", "Android", "ReactNative"], "Id": "reactnative", "Title": "React Native", "Description": "Testing of React Native", "Created": "2020-09-25", "Category": "Apps", "IsDraft": true}

# React Native

Time to learn React native. I have always thought React Native is a bloated webapp, in reality it feels like Xamarin. Just without C#. My goal is to feel the difference between Xamarin and React Native in structuring apps.

I will look into setting up React Native and creating a navigation scheme where I can read this blog in the app.

## Setup

[Getting started on Macbook Pro]](https://medium.com/@pabasarajayawardhana/react-native-environment-set-up-on-mac-os-with-xcode-and-android-studio-324e64c8552e)

Also recommend reading this [post](https://levelup.gitconnected.com/getting-started-with-react-native-in-2019-build-your-first-app-a41ebc0617e2) about understanding the concepts found in the app.


## Loading data




```javascript
    async componentDidMount() {
        try {
            const httpResponse = await fetch('uri');
            const result = await httpResponse.json();
            this.setState({state: result.data, loading: false});
        } catch(err) {
            // Retry or show cheesy message about world is down and come back alter.
        }
    }

```

## How does it work

https://blog.twitch.tv/en/2017/04/25/investigating-react-native-6032ecced610/

## Typescript

## Components

```
class Test extends Component{
  state = {
    test : 'Some text',
    index : 42,
  }
  onPress = () => this.setState({test:this.state.test + this.state.index++})
  render(){
    return (
      <View>
        <Button 
          title={this.state.test}
          onPress={this.onPress}
        />
      </View>
    )
  }
}
```

## Note to self before publishing.

https://medium.com/@alialhaddad/fetching-data-in-react-native-d92fb6876973

https://blog.jscrambler.com/how-to-set-up-and-use-navigators-in-react-native/   

https://www.npmjs.com/package/react-native-game-engine

https://blog.logrocket.com/flutter-vs-react-native-vs-xamarin/

https://www.skcript.com/svr/how-to-create-custom-component-in-react-native/
