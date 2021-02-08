<template>
  <root>
    <app-navigation></app-navigation>
  </root>
</template>

<script>
import React, { Component } from 'react';
import { StyleSheet, View, Text,Icon } from 'react-native';
import Ionicons from 'react-native-vector-icons/Ionicons';
import Entypo from 'react-native-vector-icons/Entypo';

import {
  createAppContainer,
  createStackNavigator,
  createDrawerNavigator,
  createSwitchNavigator,
  createBottomTabNavigator
} from "vue-native-router";
import { Root } from "native-base";
import Vue from "vue-native-core";

// import store from "./store";
// Vue.prototype.$store = store;

//master
import MasterScreen from "./screens/master/index.vue";

const LandingStack = createStackNavigator(
  {
    Loading: {screen: MasterScreen},
  },
  {
    initialRouteName: "Loading",
    headerMode: "none"
  });

const AuthStack = createStackNavigator(
  {
    SignIn: {screen: MasterScreen},
  },
  {
    initialRouteName: "SignIn",
    headerMode: "none"
  });

const DashboardStack = createStackNavigator(
  {
    dashboard: {screen: MasterScreen},
  },
  {
    initialRouteName: "dashboard",
    headerMode: "none"
  });

const WalletStack = createStackNavigator(
  {
    walletOverview: {screen: MasterScreen},
  },
  {
    initialRouteName: "walletOverview",
    headerMode: "none"
  });

const StakingStack = createStackNavigator(
  {
    staking: {screen: MasterScreen},
  },
  {
    initialRouteName: "staking",
    headerMode: "none"
  });

const PointStack = createStackNavigator(
  {
    point: {screen: MasterScreen},
  },
  {
    initialRouteName: "point",
    headerMode: "none"
  });
const ProfileStack = createStackNavigator(
  {
    profile: {screen: MasterScreen},
  },
  {
    initialRouteName: "profile",
    headerMode: "none"
  });

const MainTabs = createBottomTabNavigator(
  {
    Beranda: {screen: DashboardStack},
    Wallet: {screen: WalletStack},
    Staking: {screen: StakingStack},
    Digipoin: {screen: PointStack},
    Profile: {screen: ProfileStack}
  },
  {
    defaultNavigationOptions: ({ navigation }) => ({
      tabBarIcon: ({ focused, horizontal, tintColor }) => {
        const { routeName } = navigation.state;
        let IconComponent = Entypo;
        let iconName;
        if (routeName === 'Beranda') {
          iconName = `windows-store${focused ? '' : ''}`;
        } else if (routeName === 'Wallet') {
          iconName = `text-document${focused ? '' : ''}`;
        } else if (routeName === 'Staking') {
          iconName = `gauge${focused ? '' : ''}`;
        } else if (routeName === 'Digipoin') {
          iconName = `suitcase${focused ? '' : ''}`;
        } else if (routeName === 'Profile') {
          iconName = `flow-tree${focused ? '' : ''}`;
        }
        return <IconComponent name={iconName} size={25} color={tintColor} />;
      },
    }),
    tabBarOptions: {
      activeTintColor: '#9b3a9e',
      inactiveTintColor: '#8b97ad',
      activeBackgroundColor:'transparent',
      inactiveBackgroundColor:'transparent',
      showLabel: true,
      labelStyle:{color:'#8b97ad',fontWeight:'400',fontSize:12},
      labelPosition: 'below-icon',
      tabStyle:{paddingTop:10,borderTopColor:'#22335b',borderTopWidth:1},
      allowFontScaling: true,
    },
    initialRouteName: "Beranda"
  },
);

const MainDrawer = createDrawerNavigator({
  MainTabs: MainTabs
});

const AppModalStack = createStackNavigator(
  {App: MainDrawer},
  {
    mode: "modal",
    headerMode: "none"
  }
);

const App = createSwitchNavigator(
  {
    Loading: {screen: LandingStack},
    Auth: {screen: AuthStack},
    App: {screen: AppModalStack}
  },
  {
    initialRouteName: "App",
    headerMode: "none"
  });

const AppNavigation = createAppContainer(App);
export default {
  components: { Root, AppNavigation }
};
</script>
