# Lambda TypeScript 사용법

-   Lambda 콘솔에서는 TypeScript 코드를 생성할 수 없으므로 TypeScript 코드를 트랜스파일하려면 TypeScript 배포 와 함께 번들로 제공되는 esbuild 또는 Microsoft의 TypeScript 컴파일러( tsc )와 같은 컴파일러를 사용하여 js변환.

<br>

1. 디렉토리 생성후 프로젝트 시작

```shell
$ mkdir <dirName> && cd <dirName>
```

<br>

2. Type script 설치

```shell
   $ npm init -y
   $ npm install typescript --save-dev
```

<br>

3. tsconfig.json파일 생성후 아래 내용 기입

```json
{
    "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "outDir": "dist",
        "rootDir": "src",
        "strict": true
    }
}
```

<br>

4. src디렉토리를 만들고 src/index.ts파일 생성후 코드 기입

```js
export const handler = async (event: any) => {
    return {
        statusCode: 200,
        body: JSON.stringify({ message: "Hello from TypeScript Lambda!" }),
    };
};
```

<br>

5. 명령어를 이력하여 컴파일 한다. (dist디렉토리에 컴파일된 js파일이 생성됨)

```shell
$ npx tsc
```

<br>

6. dist폴더에 필요한 라이브러리 및 종속성을 설치

```shell
$ cd dist
$ npm init -y
$ npm install --production
```

<br>

7. dist디렉토리의 내용을 압축후 aws cli를 사용하여 lambda 생성

```shell
$ aws lambda create-function --function-name FUNCTION_NAME --runtime nodejs14.x --role ROLE_ARN --handler index.handler --zip-file fileb://./dist.zip
```
