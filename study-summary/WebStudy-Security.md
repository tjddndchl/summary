## Spring Security 개요

Spring Security는 Java 기반의 웹 어플리케이션에 보안 기능을 제공하는 프레임워크입니다.

### 주요 특징 및 구성 요소

1. **인증 (Authentication)**: 사용자의 신원을 확인하는 과정입니다.
2. **인가 (Authorization)**: 사용자가 특정 리소스에 접근하거나 특정 작업을 수행할 권한이 있는지 확인하는 과정입니다.
3. **SecurityContextHolder**: 현재의 보안 컨텍스트 정보를 유지합니다.
4. **Filter Chain**: 보안 관련 작업을 수행하는 서블릿 필터들의 체인입니다.
5. **UserDetails 및 UserDetailsService**: 사용자의 상세 정보를 로드하는데 사용되는 인터페이스입니다.
6. **Method-level Security**: 서비스 또는 리포지토리 계층에서 메서드 수준의 보안을 적용합니다.
7. **CSRF Protection**: CSRF 공격을 방어하기 위한 내장 기능을 제공합니다.
8. **CORS Configuration**: 다른 도메인의 리소스에 접근할 수 있도록 설정합니다.
9. **OAuth 2.0 & OIDC**: OAuth 2.0 및 OIDC 기반의 인증 및 인가를 지원합니다.

`PasswordEncoder`를 XML을 사용하여 빈으로 등록하는 방식은 주로 Spring의 전통적인 XML 기반 설정에서 사용됩니다. 아래는 `PasswordEncoder`를 XML로 빈으로 등록하는 방법을 나타냅니다:

1. **의존성 추가**: 먼저, Spring Security 의존성을 `pom.xml`에 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.x.x.RELEASE</version> <!-- 적절한 버전을 사용하세요 -->
</dependency>
```

2. **XML에서 `PasswordEncoder` 빈 등록**:

`applicationContext.xml` 또는 Spring 설정 XML 파일에서 아래와 같이 `PasswordEncoder` 빈을 등록합니다.

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- BCrypt Password Encoder 빈 등록 -->
    <bean id="passwordEncoder" class="org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder" />

</beans>
```

3. **빈 사용**:

Java 코드에서 `PasswordEncoder`를 주입받아 사용할 수 있습니다.

```java
@Autowired
private PasswordEncoder passwordEncoder;

public void registerUser(String rawPassword) {
    String encodedPassword = passwordEncoder.encode(rawPassword);
    // 저장 또는 기타 작업
}

public boolean checkPassword(String rawPassword, String storedPassword) {
    return passwordEncoder.matches(rawPassword, storedPassword);
}
```

`@Autowired` 애너테이션을 사용하여 `passwordEncoder` 빈을 주입받은 후, 인코딩 또는 검증 작업을 진행할 수 있습니다.

물론입니다. 아래는 `PasswordEncoder`의 `encode`와 `matches` 메서드의 차이점과 `matches` 메서드를 사용하는 이유에 대해 Markdown 형식으로 설명한 내용입니다:

---

## PasswordEncoder의 `encode` vs `matches`

`PasswordEncoder`는 주로 패스워드의 인코딩과 검증에 사용되는 인터페이스입니다. 이 인터페이스에서는 두 가지 주요 메서드, 즉 `encode`와 `matches`를 제공합니다.

### `encode` 메서드

- **목적**: 원본 패스워드를 인코딩(해싱)하여 저장 가능한 형태로 변환하는 데 사용됩니다.
- **사용 시나리오**: 사용자가 패스워드를 처음 설정하거나 패스워드를 변경할 때 주로 사용됩니다.
- **예시**:

  ```java
  String rawPassword = "user123";
  String encodedPassword = passwordEncoder.encode(rawPassword);
  ```

### `matches` 메서드

- **목적**: 제공된 원본 패스워드와 저장된 인코딩된 패스워드가 일치하는지 확인하는 데 사용됩니다.
- **사용 시나리오**: 사용자가 로그인할 때 주로 사용됩니다.
- **예시**:

  ```java
  boolean isMatch = passwordEncoder.matches(rawPassword, storedEncodedPassword);
  ```

## 왜 `matches`를 사용하는가?

패스워드를 검증할 때 `encode` 메서드를 사용하지 않고 `matches` 메서드를 사용하는 주요 이유는 아래와 같습니다:
1. **Salt의 고려**: 많은 해싱 알고리즘은 각각의 패스워드에 고유한 salt를 사용하여 추가적인 보안을 제공합니다. `matches` 메서드는 이 salt를 알고 있으며, 해당 salt로 원본 패스워드를 해싱한 후 저장된 해싱된 패스워드와 일치하는지 확인할 수 있습니다.
 
2. **동일한 입력, 다른 출력**: 일부 해싱 알고리즘(예: BCrypt)은 동일한 패스워드를 입력해도 매번 다른 출력(해시)을 생성합니다. 따라서 단순히 `encode` 메서드를 사용하여 같은 패스워드를 해싱하고 그 결과를 비교하는 것은 무의미합니다.
  
3. **보안**: 직접 해싱 알고리즘과 salt를 조작하려고 시도하는 것은 복잡하고, 실수로 인한 보안 취약점을 도입할 수 있습니다. `matches` 메서드는 이러한 복잡성을 추상화하여 안전하게 패스워드 일치 여부를 확인할 수 있게 해줍니다.

---

결론적으로, 패스워드 검증 시 `matches` 메서드는 안전하고 효과적인 방법으로 원본 패스워드와 저장된 해싱된 패스워드를 비교합니다. 따라서 로그인 및 패스워드 검증 작업에서는 항상 이 메서드를 사용해야 합니다.

물론입니다. 아래는 `BCryptPasswordEncoder`에 대한 설명 및 설정 방법을 Markdown 형식으로 제공한 내용입니다:

---

## BCryptPasswordEncoder 알고리즘

`BCryptPasswordEncoder`는 Spring Security에서 제공하는 BCrypt 해싱 알고리즘을 사용한 패스워드 인코딩 클래스입니다.

### BCrypt 알고리즘 특징

1. **Salted**: BCrypt는 패스워드 해싱 시 내부적으로 salt를 자동으로 생성하고 해시에 추가합니다. 이는 동일한 패스워드에 대해서도 다양한 해시 값을 생성합니다.
2. **Adaptive**: 시간이 지남에 따라 공격이 강력해질 수 있으므로, BCrypt는 "strength"(또는 "rounds") 파라미터를 통해 해싱의 복잡성을 조절할 수 있습니다.
3. **Slow**: 고의적으로 느리게 설계되어 brute-force 공격에 대한 저항력이 있습니다.

### BCryptPasswordEncoder 설정

특정 strength(라운드) 값을 사용하려면:

**XML 설정**:

`applicationContext.xml` 또는 Spring 설정 XML 파일에서 아래와 같이 빈을 등록할 수 있습니다.

```xml
<bean id="passwordEncoder" class="org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder">
    <!-- 복잡성을 조절하려면 아래 property를 설정하세요. 기본값은 10입니다. -->
    <constructor-arg name="strength" value="12" />
</bean>
```

---

`BCryptPasswordEncoder`는 손쉽게 패스워드를 안전하게 저장하고 관리할 수 있도록 도와주는 클래스입니다. 적절한 strength 값을 설정하여 애플리케이션의 보안 수준을 높일 수 있습니다.

## 단방향 암호화 vs 양방향 암호화

### 1. 단방향 암호화 (Hashing)

- **특징**: 원본 데이터를 암호화한 후에는 원래의 데이터로 복구할 수 없습니다.
- **목적**: 데이터의 무결성 및 동일성을 확인하기 위해 사용됩니다. 주로 패스워드 저장에 사용됩니다.
- **주요 알고리즘**:
  - SHA-256 (Secure Hash Algorithm)
  - SHA-3
  - BCrypt
  - Argon2
- **예시**: 사용자의 패스워드를 안전하게 저장하기 위해 해싱하여 데이터베이스에 저장.

### 2. 양방향 암호화 (Encryption)

- **특징**: 암호화된 데이터는 적절한 키를 사용하여 원본 데이터로 복구할 수 있습니다.
- **목적**: 중요한 정보를 안전하게 전송하거나 저장하고, 필요할 때 복호화하여 원본 데이터를 얻기 위해 사용됩니다.
- **주요 알고리즘**:
  - AES (Advanced Encryption Standard)
  - DES (Data Encryption Standard)
  - RSA (공개키 암호화 방식 중 하나)
  - Blowfish
- **예시**: 중요한 문서나 파일을 암호화하여 저장하고, 필요할 때만 복호화하여 열람.

---

## 주요 차이점 요약

- **복원 가능성**: 단방향 암호화는 원본 데이터로 복원할 수 없으나, 양방향 암호화는 가능합니다.
- **사용 목적**: 단방향 암호화는 주로 검증을 위해 사용되며, 양방향 암호화는 데이터의 보안을 위해 사용됩니다.
- **키의 필요성**: 단방향 암호화는 복호화 키가 필요하지 않습니다. 양방향 암호화는 암호화 및 복호화에 키가 필요합니다.

---

이와 같이 단방향 암호화와 양방향 암호화는 각기 다른 목적과 상황에 따라 선택되어 사용됩니다. 선택하기 전에 데이터의 보안 요구 사항과 활용 케이스를 고려하여 적절한 암호화 방식을 선택해야 합니다.
