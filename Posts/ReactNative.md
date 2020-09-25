{"Tags":["Mac", "React", "iOS", "Android", "ReactNative"], "Id": "reactnative", "Title": "React Native", "Description": "Testing of React Native", "Created": "2020-09-25", "Category": "Apps", "IsDraft": true}

# React Native

Time to learn React native. My goal is to feel the difference between Xamarin and React Native in creating apps fast.

I followed this guide to setup React Native on my MacBook Pro:
https://medium.com/@pabasarajayawardhana/react-native-environment-set-up-on-mac-os-with-xcode-and-android-studio-324e64c8552e


Initial work:
https://levelup.gitconnected.com/getting-started-with-react-native-in-2019-build-your-first-app-a41ebc0617e2

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


## Android and IOS

https://www.skcript.com/svr/how-to-create-custom-component-in-react-native/

#
