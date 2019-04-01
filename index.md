<script src="/qrcodejs/qrcode.min.js"></script>

<script>
(function() {
    document.getElementsByTagName("header")[0].innerHTML = '<p id="code-desc"></p><div id="qrcode"></div>';
    const qr = document.getElementById("qrcode");
    const setupBtn = document.getElementById("setup-btn");
    const resetBtn = document.getElementById("reset-btn");
    const codeDesc = document.getElementById("code-desc");
    const qrCode = new QRCode(qr, {
        text: "test",
        width: 128,
        height: 128,
        colorDark : "#000000",
        colorLight : "#ffffff",
    });
    qrCode.clear();
    const makeCode = (function(content, description) {
        qrCode.clear();
        qrCode.makeCode(content);
        codeDesc.innerHTML = description;
    });
    var progress = 0;
    const buttonName = (function() {
        if (!progress) {
            setupBtn.innerHTML = "Begin Setup";
        } else {
            setupBtn.innerHTML = "Next Step";
        }
    });
    setupBtn.onclick = (function() {
        switch (progress) {
            case 0:
                const wifi = prompt("Enter your wifi password");
                if (wifi !== null) {
                    makeCode(wifi, "wifi password");
                }
                progress++;
                break;
            case 1:
                const phone = prompt("Enter your phone number (starting with +27)");
                if (phone !== null) {
                    makeCode(phone, "phone number");
                }
                progress++;
                break;
            case 2:
                const email = prompt("Enter your email address");
                if (email !== null) {
                    makeCode(email, "email address");
                }
                progress++;
                break;
            default:
                alert("Setup complete! You will receive an email confirmation.");
                progress = 0;
                break;
        }
        buttonName();
    });
    reset.onclick = (function() {
        const pin = prompt("his QR code will clear all settings and reset the device. Enter your device pin");
        if (pin !== null) {
            makeCode(pin, "reset device");
        }
    });
    buttonName();
})();
</script>

<p><a id="setup-btn" href="#"></a></p>
<p><a id="reset-btn" href="#">Reset Unit</a></p>
<p><a href="http://18.208.169.168:5000/">Remote Arm/Disarm</a></p>
