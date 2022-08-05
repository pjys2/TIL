# nodejs로 S3에 오디오파일 업로드하기

## aws-sdk 설치
```
npm i aws-sdk
```
## fs 설치
```
npm i fs
```

## IAM계정 설정




## nodejs 코드
```nodejs
// 모듈 import 
import AWS from 'aws-sdk';
import  fs  from 'fs';

// IAM계정 생성 후 액세스 ID, key
const ID = '액세스 ID';
const SECRET = '액세스 Key';
// 버킷이름
const BUCKET_NAME = '버킷이름';

// S3 객체에 ID, Key 등록
const s3 = new AWS.S3({
    accessKeyId: ID,
    secretAccessKey: SECRET
});

const uploadFile = (fileName) => {
    // fs.readFileSync를 통해서 파일 불러오기
    const fileContent = fs.readFileSync(fileName);
    const params = {
        Bucket: BUCKET_NAME,
        Key: 'script/testAudio.wav', // 파일 Key 버킷 내 script 디렉터리에 testAudio.wav라는 파일로 들어감            
        Body: fileContent,
        ContentType: 'audio/wav'
    };
        // Uploading files to the bucket
    s3.upload(params, function(err, data) {
        if (err) {
        }
        console.log(`File uploaded successfully. ${data.Location}`);
    });
};
uploadFile('testAudio.wav');
```
