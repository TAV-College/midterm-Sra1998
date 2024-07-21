
const fs = require('fs');
const path = require('path');

const root = process.cwd();
const oldDirPath = path.join(root, 'app');
const newDirPath = path.join(root, 'app-example');
const newAppDirPath = path.join(root, 'app');

const indexContent = `import { Text, View } from "react-native";

export default function Index() {
  return (
    <View
      style={{
        flex: 1,
        justifyContent: "center",
        alignItems: "center",
      }}
    >
      <Text>Edit app/index.tsx to edit this screen.</Text>
    </View>
  );
}
`;

const layoutContent = `import { Stack } from "expo-router";

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" />
    </Stack>
  );
}
`;

fs.rename(oldDirPath, newDirPath, (error) => {
  if (error) {
    return console.error(`Error renaming directory: ${error}`);
  }
  console.log('/app moved to /app-example.');

  fs.mkdir(newAppDirPath, { recursive: true }, (error) => {
    if (error) {
      return console.error(`Error creating new app directory: ${error}`);
    }
    console.log('New /app directory created.');

    const indexPath = path.join(newAppDirPath, 'index.tsx');
    fs.writeFile(indexPath, indexContent, (error) => {
      if (error) {
        return console.error(`Error creating index.tsx: ${error}`);
      }
      console.log('app/index.tsx created.');

      const layoutPath = path.join(newAppDirPath, '_layout.tsx');
      fs.writeFile(layoutPath, layoutContent, (error) => {
        if (error) {
          return console.error(`Error creating _layout.tsx: ${error}`);
        }
        console.log('app/_layout.tsx created.');
      });
    });
  });
});





{
  "expo": {
    "name": "midterm-summer-24",
    "slug": "midterm-summer-24",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/images/icon.png",
    "scheme": "myapp",
    "userInterfaceStyle": "automatic",
    "splash": {
      "image": "./assets/images/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "ios": {
      "supportsTablet": true
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/images/adaptive-icon.png",
        "backgroundColor": "#ffffff"
      }
    },
    "web": {
      "bundler": "metro",
      "output": "static",
      "favicon": "./assets/images/favicon.png"
    },
    "plugins": [
      "expo-router"
    ],
    "experiments": {
      "typedRoutes": true
    }
  }
}


{
  "name": "midterm-summer-24",
  "version": "1.0.0",
  "scripts": {
    "reset-project": "node reset-project.js"
  },
  "dependencies": {
    "expo": "~44.0.0",
    "react": "17.0.1",
    "react-native": "0.64.3"
  }
}
