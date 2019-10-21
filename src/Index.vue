<template>
    <root>
        <app-navigator></app-navigator>
    </root>
</template>

<script>
import React from "react";
import { Platform } from "react-native";
import { Root } from "native-base";
// import { Icon } from "native-base";
import Ionicons from 'react-native-vector-icons/Ionicons';
import { createAppContainer, 
        createStackNavigator, 
        createBottomTabNavigator,
        createMaterialTopTabNavigator, } from "vue-native-router";
// tabs
import Home from "./tabs/Home";
import Settings from "./tabs/Settings";

const HomeStack = createStackNavigator(
    {
        Home: {
            screen: Home,
            navigationOptions: {
                title: 'Home',
            },
        },
    },
    {
        initialRouteName: 'Home',
        defaultNavigationOptions : {
            headerStyle: {
                backgroundColor: Platform.OS === 'ios' ? '' : '#694fad',
                marginTop: Platform.OS === 'ios' ? 0 : -24,
            },
            headerTintColor: Platform.OS === 'ios' ? '' : 'white',
        },
    },
);

const SettingsStack = createStackNavigator(
    {
        Settings: {
            screen: Settings,
            navigationOptions: {
                title: 'Settings'
            },
        },
    },
    {
        initialRouteName: 'Settings',
        defaultNavigationOptions : {
            headerStyle: {
                backgroundColor: Platform.OS === 'ios' ? '' : '#694fad',
                marginTop: Platform.OS === 'ios' ? 0 : -24,
            },
            headerTintColor: Platform.OS === 'ios' ? '' : 'white',
        },
    },
)


const androidNavigator = createMaterialTopTabNavigator (
    {
        Home: {
            screen:HomeStack,
            navigationOptions: {
                title: 'Inicio',
            },
        },
        Settings: {
            screen: SettingsStack,
            navigationOptions: {
                title: 'Configuración',
            } 
        },
    }, 
    {
        initialRouteName: 'Home',
        tabBarOptions: {
            showIcon: false,
            style: {
                // backgroundColor: '#f00',
                marginTop: 24
            }
        },
        defaultNavigationOptions: ({ navigation }) => ({
            barStyle: { backgroundColor: '#694fad' },
            tabBarIcon: ({ focused, horizontal, tintColor }) => {
                const { routeName } = navigation.state;
                let IconComponent = Ionicons;
                let iconName;
                if (routeName === 'Home') {
                    // iconName = `md-information-circle${focused ? '' : '-outline'}`;
                    iconName = `md-medkit`;
                } else if (routeName === 'Settings') {
                    iconName = `md-settings`;
                }
                return <IconComponent name={ iconName } size={ 25 } color={ tintColor }/>
            }
        })
    }
);

const iosNavigator = createBottomTabNavigator (
    {
        Home: {
            screen:HomeStack,
            navigationOptions: {
                title: 'Inicio',
            },
        },
        Settings: {
            screen: SettingsStack,
            navigationOptions: {
                title: 'Configuración',
            } 
        },
    }, 
    {
        initialRouteName: 'Home',
        defaultNavigationOptions: ({ navigation }) => ({
            // barStyle: { backgroundColor: '#694fad' },
            tabBarIcon: ({ focused, horizontal, tintColor }) => {
                const { routeName } = navigation.state;
                let IconComponent = Ionicons;
                let iconName;
                if (routeName === 'Home') {
                    // iconName = `md-information-circle${focused ? '' : '-outline'}`;
                    iconName = `md-medkit`;
                } else if (routeName === 'Settings') {
                    iconName = `md-settings`;
                }
                return <IconComponent name={ iconName } size={ 28 } color={ tintColor }/>
            }
        })
    }
);

// Dynamic navigation bar selection 
const MainNavigator = Platform.select({
    ios: iosNavigator ,
    android: androidNavigator
});

const AppNavigator = createAppContainer(MainNavigator);

export default {
    components: { Root, AppNavigator },
}
</script>