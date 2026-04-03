## 1. @Module
 - 소스를 묶는 역할
 - @Module에는 imports(다른 모듈 가져옴), controllers(컨트롤러), providers(서비스), exports(외부에서 접근 가능하게 허용) 라는게 있음
```
@Module({
  imports: [TypeOrmModule.forFeature([Mem])],
  providers: [MemService],
  controllers: [MemController],
  exports: [MemService],
})
```
## 2. @UseGuards(JwtAuthGuard)
 - 컨트롤러에서 로그인 정보가 필요할때 @UseGuards(JwtAuthGuard) 사용. 서비스는 컨트롤러에서 전달받아야됨. Request 객체에 있는 accessToken, refreshToken을 전달 받아야 하기 때문.
## 3. JWT
 ### 로그인 시 JWT 흐름
 - 로그인 요청
 -  DB에서 로그인 정보 조회 후 유효성 체크
 -   아이디로 JWT 토큰(accessToken, refreshToken) 발급. 로그아웃 처리를 위해 redis에 refreshToken 저장
 ### API 호출 시 JWT 흐름
 - API 요청 시 헤더에 accessToken 포함하여 요청
 - JwtAuthGuard, JwtStrategy에서 accessToken을 디코딩하여 memId 추출
 - memId로 db 조회하여 유효성 체크
 - @CurrentMem()으로 리턴
```
  @Get('me')
  @UseGuards(JwtAuthGuard)
  async me(@CurrentMem() mem: { memId: string }) {
    return { memId: mem.memId };
  }
```
