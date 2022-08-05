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
* 서비스에서 IAM을 검색한다
![IAM](https://github.com/JaeyeongPark/TIL/blob/main/AWS/S3/img/IAM.PNG)
* 액세스관리-사용자로 들어가서 사용자 추가 버튼을 누른다.
![사용자 추가](https://github.com/JaeyeongPark/TIL/blob/main/AWS/S3/img/%EC%82%AC%EC%9A%A9%EC%9E%90%EC%B6%94%EA%B0%80.PNG)
* 사용자이름을 입력하고 AWS자격 증명 유형에서 프로그래밍 방식 액세스를 클릭하고 다음을 누른다.
![사용자 이름](https://github.com/JaeyeongPark/TIL/blob/main/AWS/S3/img/%EC%82%AC%EC%9A%A9%EC%9E%90%20%EC%9D%B4%EB%A6%84.PNG)
* 기존 정책 직접 연결을 선택한뒤 S3를 검색해서 AmazonS3FullAcess를 체크하고 다음을 누른다.
![S3 정책설정](https://github.com/JaeyeongPark/TIL/blob/main/AWS/S3/img/s3%EC%A0%95%EC%B1%85%EC%84%A4%EC%A0%95.PNG)
* 계속해서 다음으로 넘어가면 액세스ID와 액세스 키가 나오는데 복사해서 저장한다.



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
