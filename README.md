<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Form Page</title>
    <!-- Add your CSS/JS links here, e.g., Tailwind CSS and Font Awesome -->
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
</head>
<body>
    <!-- Your form content here -->
    <script src="https://challenges.cloudflare.com/turnstile/v0/api.js" async defer></script>
    
    <div class="pt-4">
        <button 
            type="submit" 
            id="submitBtn"
            class="w-full py-4 px-4 bg-gradient-to-r from-purple-600 to-pink-600 hover:from-purple-700 hover:to-pink-700 text-white font-semibold rounded-xl shadow-lg transition-all duration-300 transform hover:scale-[1.02] flex items-center justify-center"
        >
            <i class="fas fa-bolt mr-2"></i>
            SUBMIT
        </button>
    </div>

    <!-- Cloudflare Turnstile moved to BOTTOM -->
    <div class="turnstile-container">
        <div id="turnstile-widget" class="turnstile-widget"></div>
        <input type="hidden" id="turnstileToken" name="turnstileToken" required>
        <div class="security-note">
            <i class="fas fa-shield-alt mr-1"></i>
            Protected by Cloudflare Turnstile
        </div>
    </div>

    <script>
        let turnstileWidget;
        let turnstileRendered = false;

        function onTurnstileSuccess(token) {
            document.getElementById('turnstileToken').value = token;
        }

        function resetTurnstile() {
            if (turnstileWidget && typeof turnstile !== 'undefined') {
                turnstile.reset(turnstileWidget);
                document.getElementById('turnstileToken').value = '';
            }
        }

        function renderTurnstile() {
            if (typeof turnstile !== 'undefined' && !turnstileRendered) {
                turnstileWidget = turnstile.render('#turnstile-widget', {
                    sitekey: '0x4AAAAAACVndqS4mreBFZ9g',
                    theme: 'dark',
                    size: 'normal',
                    callback: onTurnstileSuccess
                });
                turnstileRendered = true;
            }
        }

        // Call render on page load
        document.addEventListener('DOMContentLoaded', renderTurnstile);
    </script>
</body>
</html>
