# ChallengeTwo-3373322
Lexographical sorting of products

function suggestedProducts(products, searchWord) {
    // Sort products lexicographically
    products.sort();

    const result = [];
    let prefix = "";

    for (let i = 0; i < searchWord.length; i++) {
        prefix += searchWord[i];
        const suggestions = [];

        // Perform binary search to find the starting index of prefix
        let left = 0, right = products.length - 1;
        while (left <= right) {
            const mid = Math.floor((left + right) / 2);
            if (products[mid] < prefix) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        // Collect up to 3 products that match the current prefix
        for (let j = left; j < Math.min(left + 3, products.length); j++) {
            if (products[j].startsWith(prefix)) {
                suggestions.push(products[j]);
            } else {
                break;
            }
        }

        result.push(suggestions);
    }

    return result;
}
