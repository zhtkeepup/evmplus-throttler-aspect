### 代码调整

aspect/index.ts 的代码，按照视频操作有类型问题，错误信息如下：

1. ERROR AS200: Conversion from type 'u64' to 'f64' requires an explicit cast.
2. ERROR TS2322: Type '~lib/@artela/aspect-libs/components/aspect/aspect-state/MutableStateValue<u64>' is not assignable to type '~lib/@artela/aspect-libs/components/aspect/aspect-state/MutableStateValue<f64>'

- 上面的错误，1 是后面加上 as f64 处理，2 是去掉等号左侧的指定类型，然后在后面的 unwrap 后加 as f64

### 命令记录

```
npm install

npm run aspect:build
npm run account:create
        [OUT]address: 0x744ffF23F75fFb35E54eB370a1C0F1e3498302dA

sudo add-apt-repository ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install solc

npm run contract:build
npm run contract:deploy
        [OUT]contract address: 0xE13E459e4FAC10Cb83353bbE98c5ECD6875648a8
        [OUT]--contractAccount 0x744ffF23F75fFb35E54eB370a1C0F1e3498302dA --contractAddress 0xE13E459e4FAC10Cb83353bbE98c5ECD6875648a8

npm run aspect:deploy -- --interval 5 -- limit 2
        [OUT]== deployed aspectID == 0x35b69aDcB99bD8C3e8D56f08D0a3a03d6e809B14

npm run contract:bind -- --contract 0xE13E459e4FAC10Cb83353bbE98c5ECD6875648a8 --aspectId 0x35b69aDcB99bD8C3e8D56f08D0a3a03d6e809B14

npm run test -- --method increment --contract 0xE13E459e4FAC10Cb83353bbE98c5ECD6875648a8
```
