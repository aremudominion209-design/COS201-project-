import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class PrimeNumbersUpTo5000 {

    public static List<Integer> findPrimes(int limit) {
        List<Integer> primes = new ArrayList<>();
        if (limit < 2) {
            return primes;
        }

        boolean[] isPrime = new boolean[limit + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = false;
        isPrime[1] = false;

        for (int num = 2; num * num <= limit; num++) {
            if (isPrime[num]) {
                // Mark multiples of num starting from num*num as non-prime
                for (int multiple = num * num; multiple <= limit; multiple += num) {
                    isPrime[multiple] = false;
                }
            }
        }

        for (int i = 2; i <= limit; i++) {
            if (isPrime[i]) {
                primes.add(i);
            }
        }

        return primes;
    }

    public static void main(String[] args) {
        int maxRange = 5000;
        List<Integer> primes = findPrimes(maxRange);

        System.out.println("Prime numbers between 0 and " + maxRange + ":");
        for (int i = 0; i < primes.size(); i++) {
            System.out.print(primes.get(i) + (i < primes.size() - 1 ? ", " : ""));
            if ((i + 1) % 15 == 0) {
                System.out.println(); // Wrap lines for readability
            }
        }
        System.out.println("\nTotal primes found: " + primes.size());
    }
}
