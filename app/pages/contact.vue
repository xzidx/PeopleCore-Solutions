<template>
    <div class="w-full min-h-screen flex justify-center items-center bg-gradient-to-br to-indigo-100">
            

    <!-- Main Card -->
    <div class="w-[92%] max-w-[1400px] h-[600px] 
                flex rounded-[40px] overflow-hidden
                shadow-2xl border border-gray-200 bg-white">

        <!-- LEFT IMAGE -->
        <div class="w-1/2 h-full relative">
            <img src="/images/peopleCore-soution.png"
                 alt="PeopleCore Solution"
                 class="w-full h-full object-cover">
            
            <!-- Optional overlay for global look -->
            <div class="absolute inset-0 bg-gradient-to-tr 
                        from-blue-700/40 to-indigo-600/30"></div>
        </div>

        <!-- RIGHT FORM -->
        <form class="w-1/2 p-12 flex flex-col justify-center">

            <h3 class="text-4xl font-bold mb-3 text-center 
                       bg-gradient-to-r from-blue-600 to-indigo-600 
                       bg-clip-text text-transparent">
                How may we help you!
            </h3>

            <p class="text-center text-gray-500 mb-10">
                We'd love to hear from you. Send us a message.
            </p>

            <!-- Row 1 -->
            <div class="flex gap-6 mb-6">
                <input 
                    class="w-full p-4 bg-gray-50 border border-gray-200 rounded-xl
                           hover:border-blue-200 hover:bg-white hover:shadow-md
                           focus:outline-none focus:ring-1 focus:ring-blue-200 
                           focus:border-blue-200
                           transition duration-300"
                    type="text"
                    placeholder="Full Name"
                    required
                />

                <input 
                    class="w-full p-4 bg-gray-50 border border-gray-200 rounded-xl
                           hover:border-blue-200 hover:bg-white hover:shadow-md
                           focus:outline-none focus:ring-1 focus:ring-blue-200 
                           focus:border-blue-200
                           transition duration-300"
                    type="email"
                    placeholder="Email Address"
                    required
                />
            </div>

            <!-- Row 2 -->
            <div class="flex gap-6 mb-6">
                <input 
                    class="w-full p-4 bg-gray-50 border border-gray-200 rounded-xl
                           hover:border-blue-200 hover:bg-white hover:shadow-md
                           focus:outline-none focus:ring-1 focus:ring-blue-200 
                           focus:border-blue-200
                           transition duration-300"
                    type="text"
                    placeholder="Phone Number"
                    required
                />

                <select 
                    class="w-full p-4 bg-gray-50 border border-gray-200 rounded-xl
                           hover:border-blue-200 hover:bg-white hover:shadow-md
                           focus:outline-none focus:ring-1 focus:ring-blue-200 
                           focus:border-blue-200
                           transition duration-300"
                    required
                >
                    <option value="">Select Service</option>
                    <option>Solution</option>
                    <option>Business</option>
                    <option>Marketing</option>
                    <option>Planning</option>
                    <option>Design</option>
                </select>
            </div>

            <!-- Message -->
            <textarea 
                class="w-full p-4 bg-gray-50 border border-gray-200 rounded-xl h-36
                       hover:border-blue-200 hover:bg-white hover:shadow-md
                       focus:outline-none focus:ring-1 focus:ring-blue-200 
                       focus:border-blue-200
                       transition duration-300 mb-8"
                placeholder="Tell us about your project..."
                required
            ></textarea>

            <!-- Button -->
            <button 
                class="w-full py-4 rounded-xl font-semibold text-lg
                       bg-gradient-to-r from-blue-600 to-indigo-600
                       hover:from-indigo-600 hover:to-blue-600
                       text-white shadow-lg hover:shadow-xl
                       transition duration-300 transform hover:-translate-y-1">
                Send Message
            </button>

        </form>

    </div>

    
</div>
<div class="w-full flex justify-center items-center bg-gradient-to-br to-indigo-50">
    <div class="w-[92%] max-w-[1400px] h-[500px] flex rounded-[40px] overflow-hidden shadow-2xl border border-gray-200 bg-white">
        
                

    </div>      


</div>




</template>