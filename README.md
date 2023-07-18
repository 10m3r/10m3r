- 👋 Hi, I’m @10m3r
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
10m3r/10m3r is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class GUN {
    private static HashMap<String, String> users = new HashMap<>(); // Kullanıcı adı ve şifreleri saklamak için bir hashmap
    private static HashMap<String, DriverProfile> driverProfiles = new HashMap<>(); // Sürücü profillerini saklamak için bir hashmap
    private static HashMap<String, Cargo> cargos = new HashMap<>(); // Yükleri saklamak için bir hashmap

    public static void main(String[] args) {
        // Kurumsal kullanıcı ve şoför girişi için varsayılan hesaplar oluşturuyoruz
        users.put("kurumsal", "sifre123"); // Örnek kurumsal hesap
        users.put("sofor", "123456");     // Örnek şoför hesabı

        Scanner scanner = new Scanner(System.in);

        System.out.println("GÜN uygulamasına hoş geldiniz!");

        while (true) {
            System.out.println("Kullanıcı adınızı girin: ");
            String username = scanner.next();

            System.out.println("Şifrenizi girin: ");
            String password = scanner.next();

            if (login(username, password)) {
                System.out.println("Giriş başarılı!");

                if (username.equals("kurumsal")) {
                    // Şirket sahiplerinin yükleri ekleyebileceği kısım
                    System.out.println("Yük açıklaması girin: ");
                    String description = scanner.next();

                    System.out.println("Yük kategorisini seçin (ham madde, tahıllar, vb.): ");
                    String category = scanner.next();

                    Cargo cargo = new Cargo(description, category);
                    cargos.put(description, cargo);
                } else if (username.equals("sofor")) {
                    // Profil sekmesi için sürücü bilgilerini girme işlemi
                    System.out.println("Adınızı girin: ");
                    String name = scanner.next();

                    System.out.println("Soyadınızı girin: ");
                    String surname = scanner.next();

                    System.out.println("Sürücü lisans numaranızı girin: ");
                    String licenseNumber = scanner.next();

                    DriverProfile profile = new DriverProfile(name, surname, licenseNumber);
                    driverProfiles.put(username, profile);
                }

                break;
            } else {
                System.out.println("Hatalı kullanıcı adı veya şifre. Tekrar deneyin.");
            }
        }

        // Uygulama işlevleri burada devam edebilir...
    }

    private static boolean login(String username, String password) {
        // Kullanıcı adı ve şifre kontrolü yapılır
        String storedPassword = users.get(username);
        return storedPassword != null && storedPassword.equals(password);
    }

    private static class DriverProfile {
        private String name;
        private String surname;
        private String licenseNumber;

        public DriverProfile(String name, String surname, String licenseNumber) {
            this.name = name;
            this.surname = surname;
            this.licenseNumber = licenseNumber;
        }

        // Getter ve setter metodları da ekleyebilirsiniz...
    }

    private static class Cargo {
        private String description;
        private String category;

        public Cargo(String description, String category) {
            this.description = description;
            this.category = category;
        }

        // Getter ve setter metodları da ekleyebilirsiniz...
    }
}
